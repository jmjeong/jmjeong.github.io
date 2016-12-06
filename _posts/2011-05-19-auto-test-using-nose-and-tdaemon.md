---
layout: post
title: NOSE와 TDAEMON을 이용한 자동 테스트
description: 
category: python
tags: python
image:
 teaser: t-python.png
---

doctest와 unittest를 이용해서 수작업으로 test suite를 만들던 중, 이를 자동화 할 수 있는 방법을
찾다. 필요한 package는 [nose](http://somethingaboutorange.com/mrl/projects/nose)와 [tdaemon](http://pypi.python.org/pypi/tdaemon/)이다.

### Installing

	sudo pip install nose django-nose tdaemon
	django-nose install

`settings.py`에 다음 라인을 추가한다.

	TEST_RUNNER = 'django_nose.NoseTestSuiteRunner'
	INSTALLED_APPS = (
		...
		'django_nose',
		...
	)
	
### 실행

	tdaemon --test-program=django --custom-args="--with-growl"
	
	
### Growl

Mac에서 growl notification을 받기 위한 package.

	hg clone http://bitbucket.org/osantana/nosegrowl
	cd nosegrowl/nose-growl
	sudo python setup.py install
	
	
### 참고

- [http://isnomore.net/2010/08/01/automated-python-testing-nose-and-tdaemon/](http://isnomore.net/2010/08/01/automated-python-testing-nose-and-tdaemon/)
