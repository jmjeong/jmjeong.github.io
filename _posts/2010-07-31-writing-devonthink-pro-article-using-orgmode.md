---
layout: post
title: "Writing Devonthink Pro article using org-mode"
description:
category: emacs
tags: mac
---

[Devonthink (Pro)](http://www.devon-technologies.com/products/devonthink/) supports rich text format writing. But I prefer [emacs orgmode](http://orgmode.org/) format to rich text format. This elisp code is for exporting orgmode document into Devonthink document.

```lisp
(defun org-export-to-devonthink (arg)
  "Call `org-export-to-devonthink` with output to a temporary buffer.
   No file is created."
  (interactive "P")
  (let (content)
    (org-export-as-html arg nil nil "*Org HTML Export*")
    (switch-to-buffer "*Org HTML Export*")
    (setq content (buffer-string))
    (kill-buffer "*Org HTML Export*")
    (setq content (replace-regexp-in-string (regexp-quote """) """ content t t))
    (do-applescript
     (format "tell application id "com.devon-technologies.thinkpro2"
create record with {name:get title of "%s", 
type:html, source:"%s", url:"%s"} in current group
end tell
" content content (buffer-file-name)))
    )
  )
(global-set-key [f8] 'org-export-to-devonthink)
```

I bind org-export-to-devonthink to [F8] key. After writing the document, press [F8]. This script exports the orgmode article in the format of HTML and save it to the selected group in Devonthink Pro.

By `Launch URL` command in Devonthink Pro, you can jump to original orgmode article.

#### Original orgmode article

![](http://farm4.staticflickr.com/3772/13171970525_df8f81cf32_o.jpg)

#### Exported HTML article saved in Devonthink Pro

![](http://farm3.staticflickr.com/2390/13172243474_d6da5021d0_o.jpg)


