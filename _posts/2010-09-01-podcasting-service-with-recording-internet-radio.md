---
layout: post
title:  인터넷 라디오 녹음하여 PodCasting Service 하기
description: 
category: 
tags:  python
---

### 프로그램 다운로드

#### Mac

MacPorts에 mplayer-devel을 인스톨한다.  Mplayer는 snow leopard에서는 컴파일이 되지 않아서
`mplayer-devel` 버젼을 인스톨해야 한다. 

    sudo port install mplayer-devel lame

#### Linux

    sudo apt-get install mplayer lame

### 방송녹음

다음은 [녹음할 라디오 방송 주소](http://gall.dcinside.com/list.php%3Fid%3Dradio&no%3D35715&page%3D1&bbs%3D)를 알아야 한다. 
녹음할 EBS 교육방송 주소는 =mms://211.218.209.124/L-FM<sub>300k</sub>=이다. 

`record.sh` 파일을 만들어서 아래와 같이 저장한다.

    #!/bin/sh
    mplayer mms://211.218.209.124/L-FM_300k  -dumpfile `date +%Y%m%d%H%M`.mp3 -dumpstream &
    sleep 600
    kill $!

=mplayer=에 시간 간격을 정해서 녹음하는 기능이 없으므로, 백그라운드로 수행한 후, 
10분 후에 process를 kill하는 방법을 사용한다.

`chmod a+x record.sh` 하여 실행 파일을 만든 후에, crontab 에 등록한다. 
녹음된 소스는 20100901xxxx.mp3 와 같은 형태로 저장이 된다.

이렇게 저장한 파일은 mp3 format 파일인 경우에는 podcast로 읽어들여도 문제가 없는데, 
EBS 교육 방송은 asf 파일 포맷이다. 그래서 pcm 파일 format으로 저장한 다음, `lame` 프로그램을
이용하여 mp3로 변환하는 것이 좋다.

    #!/bin/sh
    cd /var/www/podcast
    FILENAME=`date +%Y%m%d%H%M`.wav
    mplayer mms://211.218.209.124/L-FM_300k -quiet -ao pcm:file=$FILENAME &
    sleep 600
    kill $!
    lame $FILENAME `basename $FILENAME .wav`.mp3
    rm $FILENAME
    python rss.py

### PodCast service

`record.sh` shell script에서 =rss.py=에 해당하는 부분이다.

RSS용 XML파일을 만들기 위해서 PyRSS2Gen이라는 package를 사용한다.
이 패키지는 =easy<sub>install</sub> PyRSS2Gen=으로 인스톨한다.

만들어진 mp3를 podcasting용 xml 파일을 만들어주는 script이다.
현재 directory에서 mp3로 끝나는 파일을 읽어서 podcast.xml 파일을 만든다.

    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    #
    # Jaemok Jeong(jmjeong@gmail.com)
    #
    # [2010/09/01]
    
    import PyRSS2Gen as RSS2
    import datetime
    
    import os,sys
    url = "http://jmjeong.com/podcast/"
    
    def main():
        """
        """
    
        mp3files = [file for file in os.listdir(".") if file.endswith(".mp3")]
    
        items = []
        for i in mp3files:
            items.append(RSS2.RSSItem(
                title = i,
                link = url+i,
                description = i,
                guid = RSS2.Guid(url+i),
                enclosure = RSS2.Enclosure(url+i, os.path.getsize(i), "audio/mpeg/"),
                pubDate = datetime.datetime.utcfromtimestamp(os.stat(i).st_ctime)))
    
    
        rss = RSS2.RSS2(
            title = "EBS podcast by jmjeong",
            link = "http://jmjeong.com/podcast/podcast.xml",
            description = "Internet EBS podcasting",
            lastBuildDate = datetime.datetime.utcnow(),
    
            items = items);
    
        rss.write_xml(open("podcast.xml", "w"), encoding = "utf-8")
    
    if __name__ == '__main__':
        main()

### Crontab에 등록

    jmjeong@jmhost:/var/www/podcast$ crontab -e
    50 6 * * * /var/www/podcast/record.sh 2>&1 /dev/null   
