---
layout: post
title: RESTful API using django
description: 
category: python
tags: python
image:
 teaser: t-python.png
---

REST API를 지원하는 server가 필요해서 django로 구성 가능한 몇가지 framework (django-piston,
django-tasypie, django-rest-framework)을 테스트 해 봤다. 세가지 framework 중에서 django-piston을
이용해서 작업을 했는데, 나중에는 django-rest-framework으로 변환할까 생각중이다.

<!-- more -->

### django-piston

두개의 테이블(user, rule)과 10여개의 API set을 가진 서버를 구성하는데, 반나절 남짓의 작업으로
가능했다. 2011.10월 시점으로 공식적으로 v0.2.2버전이 release 되었다. 개발은 쉽고 편했는데, 2년여간
update가 되지 않았고, 문서가 상대적으로 빈약했다. 최근에 새로운 maintainer가 코드를 인수인계 받아서
update가 기대되고 있다.

#### urls.py

{% highlight python %}
from piston.resource import Resource
from latte.api.handlers import UserHandler, RuleHandler, RuleSearchOwnerHandler, RuleSearchTargetHandler

class CsrfExemptResource(Resource):
    """A Custom Resource that is csrf exempt"""
    def __init__(self, handler, authentication=None):
        super(CsrfExemptResource, self).__init__(handler, authentication)
        self.csrf_exempt = getattr(self.handler, 'csrf_exempt', True)
 
user = CsrfExemptResource(UserHandler)

urlpatterns = patterns('',
    url(r'^user/?$', user),
    url(r'^user/(?P<email>[^/]+)/?$', user),
)
{% endhighlight %}

#### handler.py

{% highlight python %}
from piston.handler import BaseHandler, AnonymousBaseHandler
from piston.utils import rc, require_mime, require_extended

from django.contrib.auth.models import User
from latte.api.models import Rule

class UserHandler(BaseHandler):
    """
    EntryPoint for registration
    """

    allowed_methods = ('GET', 'POST', 'DELETE')
    fields = ('email',)

    def read(self, request, email=None):
        """
        """
        if not email:
            return User.objects.filter(is_superuser=False)

        try:
            return User.objects.get(email=email,is_superuser=False)
        except (User.DoesNotExist, KeyError):
            return rc.NOT_FOUND


    def delete(self, request, email=None):
        """
        """
        if not email:
            return rc.BAD_REQUEST

        try:
            user = User.objects.get(email=email,is_superuser=False)
        except (User.DoesNotExist):
            return rc.NOT_FOUND

        user.delete()
        return rc.DELETED

    def create(self, request):
        """
        Process connection : register user with email and password
        """

        if not request.content_type:
            return rc.BAD_REQUEST
            
        data = request.data

        try:
            user = User.objects.get(username=data['email'])
            return rc.DUPLICATE_ENTRY
        except (User.DoesNotExist, KeyError):
            user = User(username=data['email'], email=data['email'])

        try:
            user.set_password(data['password'])
            user.save()
        except KeyError:
            return rc.BAD_REQUEST
            
        return rc.CREATED
{% endhighlight %}
		
#### django-tastypie

v1.0.0-beta 버전이 release 되었다. dehydrate, hydrate function에서 GET과 PUT에 대한 세부적인 제어를
하게 되어 있다.


#### urls.py

{% highlight python %}
from django.conf.urls.defaults import *
from tastypie.resources import ModelResource
from tastypie.api import Api

from api.resources import UserResource, RuleResource

from django.contrib import admin
admin.autodiscover()

v1_api = Api(api_name='v1')
v1_api.register(UserResource())

urlpatterns = v1_api.urls
{% endhighlight %}

#### resources.py

{% highlight python %}
from django.contrib.auth.models import User
from latte.api.models import Rule

from tastypie.resources import ModelResource
from tastypie.authorization import Authorization
from tastypie import fields
from tastypie import http

class UserResource(ModelResource):
    class Meta:
        queryset = User.objects.filter(is_superuser=False)
        list_allowed_methods = ['get', 'post']
        detail_allowed_methods = ['get', 'post']
        excludes = ['id']
        resource_name = 'user'
        include_resource_uri = False
        authorization = Authorization()
        fields = ['username']

    # def hydrate(self, bundle):
    #     bundle.obj.email = bundle.data['username']
        
    #     return bundle

    def obj_create(self, bundle, request=None, **kwargs):
        try:
            user = User.objects.get(username=bundle.data['email'])
            return http.HttpConflict()
        except (User.DoesNotExist, KeyError):
            user = User(username=bundle.data['email'], email=bundle.data['email'])
        
        bundle.obj = user
        return bundle
...
{% endhighlight %}

### django-rest-framework

앞의 두 framework 대비해서 자동으로 API 접근에 관한 문서를 만들어주는 장점이 있다. Django의 class
based view에 기반을 해서 간단하고, 모듈화 된 장점도 있다.

#### urls.py

{% highlight python %}
from django.conf.urls.defaults import *

from djangorestframework.resources import ModelResource
from djangorestframework.views import ListOrCreateModelView, InstanceModelView

from latte.api.resources import RuleResource
from latte.api.views import TestView

urlpatterns = patterns('',
    url(r'^test/$', TestView.as_view(), name="test"),
                       
    url(r'^rule/$', ListOrCreateModelView.as_view(resource=RuleResource), name="rule-list"),
    url(r'^rule/(?P<pk>[^/]+)/$', InstanceModelView.as_view(resource=RuleResource),
    name="rule-detail"),
...
)
{% endhighlight %}

#### views.py

{% highlight python %}
from django.core.urlresolvers import reverse

from djangorestframework.views import View
from djangorestframework.response import Response
from djangorestframework import status

from latte.api.models import Rule

class TestView(View):
    """
    TestView basic
    """
    # model = Rule
    fields = ('title', 'when', 'where', 'message')
    
    def get(self, request):
        """
        Handle Get requests
        """

        # print request.data
		return Rule.objects.all()
{% endhighlight %}
