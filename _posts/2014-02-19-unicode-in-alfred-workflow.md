---
layout: post
title: "alfred workflow의 한글 처리"
description: ""
tags: alfred python
---

Mac에서 alfred workflow를 만들다보면 한글 argument 비교 처리가 안 되는 현상이 있습니다. Mac에서
unicode를 NFD(Normalization Form Decomposition)으로 처리를 해서 생기는 문제입니다. Windows나 python
등에서는 NFC로 처리가 됩니다.

- [관련글 - alfredtweet 한글 자소 풀림]({% post_url 2012-03-23-korean-patch-in-alfred-tweet %} )

alfred 인자로 받은 string을 NFC로 변경해주면 비교가 가능합니다. 마찬가지로 맥에서 한글 파일명을
처리할 때에도 NFD로 변환한 후 처리해야 합니다. 

```py
import unicodedata

q=u”{query}”
q=unicodedata.normalize(‘NFC’, q)
```

