---
layout: single
title: TDD in django
description: 
category: python
tags: python
---

doctest와 unittest 방법이 있다. 여기서는 unittest에 대해서 정리한다.

<!-- more -->

### Writing tests

```python
import unittest

class MyFuncTestCase(unittest.TestCase):
    def testBasic(self):
        a = ['larry', 'curly', 'moe']

        self.assertEquals(my_func(a, 0), 'larry')
        self.assertEquals(my_func(a, 1), 'curly')
```

### Writing unit tests

test runner는 수행할 때 두 장소에서 `unit tests`를 찾는다.

- **models.py** : 이 모듈에서 unittest.TestCase의 subclass를 찾는다
- **tests.py** in application directory : models.py가 위치한 directory. 여기서도 unittest.TestCase의 subclass를 찾는다.

```python
import unittest
  
from myapp.models import Animal
  
class AnimalTestCase(unittest.TestCase):
    def setUp(self):
        self.lion = Animal.objects.create(name='lion', sound='roar')
        self.cat = Animal.objects.create(name='cat', sound='meow')
  
    def testSpeaking(self):
        self.assertEquals(self.lion.speak(), 'The lion says "roar"')
        self.assertEquals(self.cat.speak(), 'The cat says "meow"')
```
		
### Running tests

	./manage.py test
	./manage.py test animal
	
### The test database

Test 데이타베이스는 실제 production database가 사용되지 않고, 매번 test database가 만들어진다.

### Testing tools

#### The test clients

test client는 더미 웹 브라우저처럼 동작하는 Python class이다. 이를 통해 Django application을 뷰를 보거나 상호작용하는 것처럼 할 수 있다.

- GET, POST request를 처리하여 결과를 볼 수 있고,
- 특정 URL을 통해 정확한 View가 수행되었지 테스트하거나
- 주어진 requests가 주어진 django template에 의해 처리가 되는지 테스트를 할 수 있다.

```python
>>> from django.test.client import Client
>>> c = Client()
>>> response = c.post('/login/', {'username': 'john', 'password': 'smith'})
>>> response.status_code
200
>>> response = c.get('/customer/details/')
>>> response.content
'<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 ...'
```

### 참고

- [http://docs.djangoproject.com/en/1.1/topics/testing/#topics-testing](http://docs.djangoproject.com/en/1.1/topics/testing/#topics-testing)
- [http://docs.python.org/library/unittest.html](http://docs.python.org/library/unittest.html)
- [http://od-eon.com/blogs/tudor/test-driven-development-django-way/](http://od-eon.com/blogs/tudor/test-driven-development-django-way/)
- [http://od-eon.com/blogs/tudor/story-test/](http://od-eon.com/blogs/tudor/story-test/)