---
layout: post
title: "PlanBe QuickAdd Tweak"
description: ""
category: ios
tags: ios jailbreak planbe
---


Jailbreak된 iOS 기기에서 PlanBe에 일정이나 할 일을 기록하는 tweak 입니다. Activator를 이용하여 지정된 키를 누르면
바로 입력이 가능합니다.

저는 Volume Down 키에 적용을 해 두었습니다. 언제라도 Volume Down key를 누르면 일정이나 할일을
입력하기 위한 창이 뜨고 `Events`, `Tasks` 버튼을 누르면 PlanBe가 구동이 되면서 일정과 할일이
입력됩니다.

PlanBe의 QuickAdd에서 사용되는 [모든 syntax]({% post_url 2014-01-19-PlanBe-QuickAdd %})가 동일하게 적용됩니다. 

<!-- more -->

![](http://farm8.staticflickr.com/7389/13240166863_677cb30fbc_o.png)

<!-- [http://cydia.myrepospace.com/jmjeong/](http://cydia.myrepospace.com/jmjeong/) 을 추가하고 'PlanBe -->
<!-- QuickAdd'를 인스톨 하면 됩니다.  설치 후에 Preferences - Activator 에서 호출할 Action을 등록하면 -->
<!-- 됩니다. -->

BigBoss에서 PlanBe QuickAdd를 검색 후에 인스톨하면 됩니다. 설치 후에 'Preferences-Activator'에서
호출할 Action을 등록하고 사용하면 됩니다.

- [Download Link](http://moreinfo.thebigboss.org/moreinfo/depiction.php?file=planbequickaddDp)
- Credits : ThereIsPlanBe 위젯을 만들고 공개한 위쯔님께 돌립니다. 

---

### Program Source

- [GitHub Link](https://github.com/jmjeong/PlanBeQuickAdd)

### Build 및 제작 과정

- [iosopendev.com](http://www.iosopendev.com)
  - [Download](http://iosopendev.com/download/) : iOSOpenDev 1.6-2 Installer install
- `iod-setup base`
- 'iod-setup sdk`
- 인스톨 할 장치에 `openssh` 인스톨 후에 ~root/.ssh에 `authorized_keys`에 접속할 device의 public key를 등록
- .bash_profile에 `iOSOpenDevDevice`에 IP 지정
{% highlight console %}
	export iOSOpenDevDevice=192.168.0.100
{% endhighlight %}
- Product - Build for - Profiling 을 수행하면, Device에 자동으로 Install
