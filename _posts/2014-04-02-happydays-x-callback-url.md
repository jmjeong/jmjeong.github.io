---
layout: post
title: "HappyDays x-callback-url"
description:
category: [happydays,ios]
tag: happydays
---

## x-callback-url 

### parse

	happydays://x-callback-url/parse?tags=&data=&prompt=&x-source=&x-success=

* tags : Tags which will be assigned to the created record
    - Case-sensitive. Delimeter ','
    - example : tags=Family,Friend
* data : Several data can be input by new line
    - format :  name,date[d-day]
    - lunar date starts with '-'. ex)-8/15
    - You can use '/', '.' and '-' for date formatter. ex)1.10
    - example
        - Tom birthday,2010/2/2
        - Thanksgiving Day,-8/15
        - Son 100th anniversary,2012/5/5[100]
* x-success
    - designate URI performed after processing
    - example : x-success={{drafts://}}
* prompt : y or n
    - Will show a pop-up window asking to go back to x-success after processing
    - example : prompt=y
* x-source :  designate name of calling App
    - for showing it on a pop-up window
    - example : xsource=Drafts

### search

	happydays://x-callback-url/search?q=&tag=

* q : Search name
* tag : Specifies the tag for searching. All data will be searched without it.
