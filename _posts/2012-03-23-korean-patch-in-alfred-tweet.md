---
layout: post
title: alfred tweet 한글 패치
description: 
category: 
tags: alfred
---

# 증상

-   [맥에서 한글이 자소 단위로 풀어지는 현상](http://namoda.springnote.com/pages/4922363)

![img](//farm8.staticflickr.com/7077/7007470163_39924ff61d_o.jpg)

![img](//farm8.staticflickr.com/7073/7007485345_7446e4a659_o.jpg)

AlfredTweet에서 posting한글이 WinXP에서 볼 때 자소 단위로 풀어지는 현상을 @gypark님이
알려주셨습니다.

Mac이나 Win7에서는 문제가 없는데 Win XP에서 볼 때에만 풀어서 보이게 됩니다.  Mac에서 unicode를
NFD(Normalization Form Decomposition)방식으로 처리하는데 Win XP에서는 이것을 자동으로 NFC로 바꿔주지
않아서 생기는 문제입니다.

AlfredApp 제작자에게 parameter를 넘길때 NFC로 넘기는 Option을 만들어달라는 건의 메일을 보냈는데,
extension client에서 처리하는게 나을것 같다는 답장이 왔습니다.  Client에서 처리하는게 맞을 것 같기도
하고요.

# 패치

## php-intl module install

Mac Lion에 있는 php는 default로 intl 모듈을 지원하지 않아서, 
php-intl 모듈을 먼저 활성화 해야 합니다.

    Jaemok-Jeong-ui-MacBook-Pro:~ jmjeong$ php -v
    PHP 5.3.8 with Suhosin-Patch (cli) (built: Nov 15 2011 15:33:15) 
    Copyright (c) 1997-2011 The PHP Group
    Zend Engine v2.3.0, Copyright (c) 1998-2011 Zend Technologies
	
-   Download and install [ICU](http://download.icu-project.org/files/icu4c/4.8.1.1/icu4c-4_8_1_1-src.tgz)

```sh
tar zxvf icu4c-4_8_1_1-src.tgz
cd icu/source
./configure
make
sudo make install
```sh
	
-   Download [php-5.3.6.tar.gz](http://kr.php.net/get/php-5.3.6.tar.gz/from/a/mirror)

```sh
cd ext/intl
phpize
./configure --enable-intl
make
```sh

-   turn on intl.so
```sh
in /etc/php.ini
add 'extension=intl.so'
```

-   확인

```sh
Jaemok-Jeong-ui-MacBook-Pro:~ jmjeong$ php -i | fgrep intl
intl
intl.default_locale => no value => no value
intl.error_level => 0 => 0
```

## AlfredTweet patch

AlfredTweet 1.5 버전에 대한 patch입니다.

```sh
diff --git a/script.php b/script.php
index fd6cc14..dd9931d 100755
--- a/script.php
+++ b/script.php
@@ -910,11 +910,15 @@

        // create a new instance
        $tweet = new TwitterOAuth($ckey1, $ckey2, $auth['oAuthKey'], $auth['oAuthSecret']);
-       $tweet_text = $text;
+
+        if (!Normalizer::isNormalized($text, Normalizer::FORM_C)) {
+            $text = Normalizer::normalize($text, Normalizer::FORM_C);
+        }
+        $tweet_text = $text;
        $tweets = array();

        // Check tweet length and break it into multiple tweets if needed.
-       if (strlen($tweet_text) > 140 && $settings->split_tweets == 1) {
+       if (mb_strlen($tweet_text, "utf-8") > 140 && $settings->split_tweets == 1) {

            // Set the regex pattern to grab mentions from the total tweet
            // then grab all mentions as an array, and reassemble as a string.
@@ -940,7 +944,7 @@

                // Check the tweet length with the new word added. Set to 136 instead of 140
                // characters to compensate for the counter at the end.
-               if (strlen($temp) > 136) {
+               if (mb_strlen($temp, "utf-8") > 136) {

                    // If its over 136 characters, then break here and make the current value its
                    // own tweet. Then reset the $newtweet value with the mentioned users in the
```
