---
layout: post
title: Gmail 정리하기
description: 
category: python
tags: python
---

회사 메일을 forward해서 사용하고 있는 gmail을 7571MB중에서 7449MB를 썼다. Gmail에 특정 날짜 이전의
메일을 정리하는 기능이 없어서 만든 script이다. 프로그램을 수행하면, 2010년 1월 1일 이전의 메일을 전부
휴지통으로 이동한다.

Gmail은 `imap.store('+FLAGS', 'Deleted')` 후에 `imap.expunge()`를 하더라도 실제 메일을 삭제하는 것이
아니라, 해당 메일에서 라벨만 제거하는 식으로 동작을 한다. 지우기 위해서는 메시지를
‘[Gmail]/Trash’로 이동한 후, 휴지통에서 삭제하는 방식을 사용해야 한다.

휴지통 이름은 ‘언어설정’에 따라 달라지는 것 같다. 한국어로 설정했을 때는 결과값이 실패로 넘어오는데, 영문으로 바꾼 후에는 정상 동작한다.

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# Copyright 2011 Jaemok Jeong(jmjeong@gmail.com)
#
# purgegmail.py
#
# Google mail purge utility
#
# [2011/04/19]

import imaplib
import datetime
import getpass
import sys

# add user information
gmail_user = ''                         # gmail account
gmail_pass = ''                         # gmail passwd
purgeDate = datetime.date(2010,01,1)    # 이 날짜 앞의 메일들은 전부 삭제

# constant
gmail_host = 'imap.gmail.com'

def process():
    imap = imaplib.IMAP4_SSL(gmail_host)

    try:
        imap.login(gmail_user, gmail_pass)
    except:
        print "Login failed"
        sys.exit(-1)

    num = imap.select()

    searchString = ('(before "%s")' % purgeDate.strftime("%d-%b-%Y"))
    typ, data = imap.search (None, searchString)

    y_or_n = raw_input("Delete %d messages? " % len(data[0].split(' ')))
    if (not (y_or_n == 'y' or y_or_n == 'Y')): return

    data = ','.join(data[0].split(' '))
    typ, data = imap.copy(data, '[Gmail]/Trash')
    if typ == "OK":
        print "Delete sucessful!"
    else:
        print "Delete failed!"

    imap.close()
    imap.logout()

if __name__ == '__main__':
    if gmail_user == '':
        gmail_user = raw_input('gmail id: ')
    if gmail_pass == '':
        gmail_pass = getpass.getpass()
        
    process()
    print "Finished..."
{% endhighlight %}
