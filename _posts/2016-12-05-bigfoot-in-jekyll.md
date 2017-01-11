---
layout: post
title: Jekyll에 bigfoot plugin 적용
description: 
category: jekyll
tags: jekyll bigfoo
---

bigfoot은 각주를 팝오버 창으로 띄워 문서의 아래로 내려가지 않고서도 내용을 확인할 수 있게 하는 jQuery plugin이다. 

![](https://zippy.gfycat.com/EachEagerEuropeanpolecat.gif)

- 참고 : [http://www.halryang.net/Bigfoot-footnotes-in-Jekyll/](http://www.halryang.net/Bigfoot-footnotes-in-Jekyll/)

## minimal mistake theme에 bigfoot 적용

- [Download bigfoot](http://www.bigfootjs.com/)[^1] 
- `cp dist/bigfoot.min.js assets/js/plugins/bigfoot.min.js`
- `cp dist/bigfoot-default.scss _sass/_bigfoot-default.scss`
- add bigfoots configuration in `_include/scripts.html`

```html
	<script type="text/javascript">
	    var bigfoot = $.bigfoot(
	        {
	        actionOriginalFN: "ignore",
	        positionContent: "false",
	        allowMultipleFN: "true",
	        activateOnHover: "true", 
	        deleteOnUnhover: "true"        
	        }
	    );
	 </script>
```

- change package.json to rebuild `assets/js/main.min.js` 

```js
	"uglify": "uglifyjs assets/js/vendor/jquery/jquery-1.12.4.min.js 
		assets/js/plugins/bigfoot.min.js assets/js/plugins/jquery.fitvids.js 
		assets/js/plugins/jquery.greedy-navigation.js 
		assets/js/plugins/jquery.magnific-popup.js 
		assets/js/plugins/jquery.smooth-scroll.min.js 
		assets/js/plugins/stickyfill.min.js assets/js/_main.js 
		-c -m -o assets/js/main.min.js",
```

- npm install -g uglifyjs 
- npm run build.js
- update `assets/css/main.scss`

```scss
	@import "bigfoot-default";
```

[^1]: A JQuery plugin for empowering footnotes

