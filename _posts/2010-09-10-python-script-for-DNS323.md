---
layout: post
title: DNS-323에서 파일정리
description: 
category: python
tags: python
---

XBMC에서 사용되는 TV Series와 Movie directory에 symbolic link를 만들기 위해 사용하는 script.
Source directory에서 이미 처리가 되지 않는 파일이 있으면 어느쪽으로 symbolic link를 만들건지
물어보고 사용자 입력을 받아서 symbolic link를 만들어주는 간단한 프로그램이다.

DNS-323에서 파일 정리를 하기 위해 사용한다.

```python
    #!/usr/bin/python
    # -*- coding: utf-8 -*-
    
    # cleanup dns-323 directory 
    # jmjeong@gmail.com ([2010-08-05 Thu])
    
    import os,sys
    import os.path
    import cPickle
    
    tvdir = "/mnt/HD_b2/TV"
    moviedir = "/mnt/HD_b2/Movie"
    sourcedir = "/mnt/HD_a2/Source"
    
    dataFile = "/mnt/HD_a2/Source/ignore.dump"
    
    def main():
        """
        """
    
        tv = os.listdir(tvdir)
        movie = os.listdir(moviedir)
        source = os.listdir(sourcedir)
    
        ignoreFiles = []
    
        try:
            ignoreFiles = cPickle.load(open(dataFile), 'r+')
        except IOError:
            pass
    
        processing = set(source) - set(tv) - set(movie) - set(ignoreFiles) 
    
        for f in processing:
            ans = ""
            try:
                print "[%s]" % f
                ans = raw_input("1.TV, 2.Movie, 3.Ignore ? (1..3): ")
            except:
                print str(sys.exc_info())
    
            if (ans == '1'):
                os.symlink(os.path.join(sourcedir,f), os.path.join(tvdir, f))
            elif (ans == '2'):
                os.symlink(os.path.join(sourcedir,f), os.path.join(moviedir, f))
            else:
                ignoreFiles.append(f)
    
        cPickle.dump(ignoreFiles, open(os.path.join(dataFile), 'w'))
    
    if __name__ == '__main__':
        main()
```
