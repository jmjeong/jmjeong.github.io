---
layout: post
title: alfred-pinboard
description: ""
tags: alfred pinboard python
image:
 teaser: t-alfred-pinboard-1.png
---

# Introduction 

Yet another alfred2-pinboard workflow. It provides INSTANT pinboard search and the following function.

- search pinboard
- search tag 
- search description 
- delete searched bookmark 
- copy url of bookmark
- send to pocket

<!-- more -->

- [Github Link](https://github.com/jmjeong/alfred-extension/tree/master/pinboard)

# Installation 

- pbauth username:TOKEN <- set access token
  - Get it from [https://pinboard.in/settings/password](https://pinboard.in/settings/password)
- pbreload - loads latest bookmarks from pinboard.in

- (optional) pbauthpocket 
  - needed only if you want to send URL to pocket
- (optional) install cron job  : for faster search without pbreload
  - */15 * * * * (curl 'https://api.pinboard.in/v1/posts/all?format=json&auth_token=username:TOKEN' > ~/.bookmarks.json) > /dev/null 2>&1
  - get it from [https://pinboard.in/settings/password](https://pinboard.in/settings/password)
 
- [Workflow Download](https://raw.github.com/jmjeong/alfred-extension/master/pinboard/pinboard.alfredworkflow)

# Command

- **pba** *query* : search *query* from description and link and tags
- **pbt** *query* : search *query* from description(title)
- **pbl** *query* : search *query* from link
- **pbd** *query* : search *query* from extended field
- **pbu** *query* : search *query* from description(title) in unread list
- **pbtag** *query* : search tag list. You can autocomplete it by pressing 'tab'
- **pbreload** : loads latest bookmarks from pinboard.in
- **pbauth** *username:token* : Set pinboard authentication token (optional)
- **pbauthpocket** : Pocket authentication (optional)
- ctl-shift-cmd-p : launch **pba** (reset when importing)
- ctl-shift-cmd-c : launch **pbtag** (reset when importing)

# Action

- *enter* to open the selected url in the browser
- Hold *cmd* while selecting a bookmark to copy it’s url to clipboard
- Hold *alt* while selecting to delete a bookmark from your pinboard
- Hold *shift* while selecting to send URL to pocket. You need to set auth_token using **pbauthpocket**
