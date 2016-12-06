---
layout: post
title: Reverse Geocoding
description: 
category: python
tags: python
---

### 역 지오코딩(주소조회)

- http://code.google.com/intl/ko/apis/maps/documentation/geocoding/index.html#ReverseGeocoding

지도 위에 위치를 읽을 수 있는 주소로 변환하는 과정을 역 지오코딩이라고 합니다. 이런 일을 하는
googlemaps라는 클래스가 있는데, 반환되는 주소가 영문으로 나옵니다. maps.google.co.kr를 사용하는
간단한 Gmaps 모듈을 만들었습니다. 반환값을 파싱하기 위해 Python 2.6부터 들어간 json 모듈을
사용했는데, 2.5 이하에서는 simplejson과 같은 모듈을 사용하시면 됩니다.

#### 사용법

	>>>  import Gmaps
    >>>  gmaps = Gmaps()
    >>>  addrLists = gmaps.reverse_geocode(37.2983333,126.835000)
    >>>  print addrList[2].encode('utf-8')
    대한민국 경기도 안산시 상록구 사동

#### 소스 (Gmaps.py)

{% highlight python %}
#!/usr/bin/env python
# -*- coding: utf-8 -*-
#
# Copyright 2010 Jaemok Jeong(jmjeong@gmail.com)
# Gmaps.py is freely available for all users under a BSD license
#
#
# Reverse Geocoding : Gmap service를 이용한 reverse geocoding
# 참고 : http://code.google.com/intl/ko-KR/apis/maps/documentation/geocoding/
#
#    (37.127,127.45) -> 대한민국 충청남도 금산군 금성면 상가리 282
#
# [2010/10/14]

import urllib,urllib2
import sys

try:
    import json
except ImportError:
    raise ImportError, "Python 2.6+ has built-in json module"

class GmapsNetworkErrorException(Exception):
    pass
class GmapsInvaidQueryException(Exception):
    pass

class Gmaps(object):
    """
    Convert a (latitude, longitude) pair to address

    >>> gmaps = Gmaps()
    >>> address = gmaps.reverse_geocode(37.2983333,126.835000)
    >>> print address[2].encode('utf-8')
    대한민국 경기도 안산시 상록구 사동
    """
    
    def __init__(self, api_key='', base_url="http://maps.google.co.kr"):
        self.api_key = api_key
        self.base_url = base_url

    def reverse_geocode(self, lat, lng, sensor="false", oe='utf8',ll='',spn='',gl=''):
        opener = urllib2.build_opener()
        urlBase = self.base_url + "/maps/api/geocode/json?%s"
        requestData = urllib.urlencode({
            'latlng': "%f,%f" % (lat,lng),
            'sensor': sensor,
            'oe' : oe,
            'll' : ll,
            'gl' : gl
        })
        requestUrl = urlBase % requestData
        
        try:
            urlHandle = opener.open(requestUrl)
        except urllib2.HTTPError, urlib2.URLError:
            raise GmapsNetworkErrorException
        
        result = json.loads(urlHandle.read())
        if result['status'] == u'OK':
            ret = []
            for i in xrange(len(result['results'])):
                ret.append(result['results'][i]['formatted_address'])
            return ret
        else:
            raise GmapsInvaidQueryException, "Invalid Query exception"
        
if __name__ == '__main__':
    # gmaps = Gmaps()
    # print gmaps.reverse_geocode(37.2983333,126.835000)[2].encode('utf-8')
    pass
{% endhighlight %}	
