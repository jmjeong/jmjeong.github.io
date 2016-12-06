---
layout: post
title: pebble-development
modified: 
category: pebble
tags: 
image:
  teaser: t-pebble.jpg
---

### 개발 환경 인스톨 in Mac

```sh
brew install pebble/pebble-sdk/pebble-sdk
git clone https://github.com/pebble/pebblejs/
edit src/js/app.js
pebble build
pebble install
```

```
[ERROR   ] Could not connect to phone at localhost:12342. Ensure that 'Developer Connection' is enabled in the Pebble app.
```

오류 발생 시 library update

```
brew update && brew upgrade glib
```

clang이 인스톨되어 있지 않다는 message가 나올 때
```
xcode-select  --install
```
