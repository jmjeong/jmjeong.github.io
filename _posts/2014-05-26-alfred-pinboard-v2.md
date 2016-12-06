---
layout: post
title: alfred-pinboard version 2
description: 
category: 
tags: alfred pinboard python
image:
 teaser: t-alfred-pinboard-2.jpg
---

### Introduction 

Yet another alfred-pinboard workflow. It provides INSTANT pinboard search and the following function.

- search pinboard (`pba`) - supports various search condition such as `or(|)`, `and( )`, and `not(-)`
- search tag (`pbtag`)
- search pinboard memo (`pbmemo`)
- show starred bookmark (`pbs`)
- browse and search history (`pbhis`)

- goto or delete the searched bookmark 
- copy url of the searched bookmark
- send url to pocket
- mark or unmark the favorite bookmark

![screenshot](https://raw.github.com/jmjeong/alfred-extension/master/alfred-pinboard/search.jpg)

### Installation 

0. Download and Install [alfred-pinboard Workflow](https://raw.github.com/jmjeong/alfred-extension/master/alfred-pinboard/pinboard.alfredworkflow)
	- You need to set short-key manually
1. pbauth username:TOKEN <- set access token
    - Get it from [https://pinboard.in/settings/password](https://pinboard.in/settings/password)
2. pbreload - loads latest bookmarks and memo from pinboard.in
3. search with `pba`, `pbtag`, `pbmemo` command

---

- (optional) pbauthpocket 
    - needed only if you want to send URL to pocket
- (optional) install cron job  : for faster searching without pbreload
    - download it from [pinboard-download.py](https://raw.github.com/jmjeong/alfred-extension/master/alfred-pinboard/pinboard-download.py)
    - `chmod a+x pinboard-download.py`
    - register script in crontab using `crontab -e`
	
      `*/15 * * * * /path/to/pinboard-download.py > /dev/null 2>&1`
	
### Command

- **pba** *query* : search *query* from title, description and tags
- **pbnote** *query* : search *query* from pinboard notes
- **pbu** *query* : search *query* from description(title) in unread list
- **pbl** *query* : search *query* from link
- **pbs** *query* : search *query* from starred bookmarks
- **pbtag** *query* : search tag list. You can autocomplete it by pressing 'tab'

- **pbhis** : show search history

- **pbreload** : loads latest bookmarks from pinboard.in

- **pbauth** *username:token* : Set pinboard authentication token (optional)
- **pbauthpocket** : Pocket authentication (optional)

### Search Condition

- `-` before search word stands for **not** `ex) -program`
- ` ` stands for **and** query `ex) python alfred`
- `|` stands for **or** query `ex) python|alfred`
- **and** query is evaluated first, than **or** query is evaluated

### Keys 

You need to set it manually because of alfred restriction

- ctl-shift-cmd-p : launch **pba** 
- ctl-shift-cmd-c : launch **pbtag** 
- ctl-shift-cmd-n : launch **pbnote**
- ctl-shift-cmd-s : launch **pbs**
- ctl-shift-cmd-h : launch **pbhis**

### Action

- *enter* to open the selected url in the browser
- *tab* to expand in pbtag command
- Hold *cmd* while selecting a bookmark to copy it’s url to clipboard
- Hold *alt* while selecting to delete a bookmark from your pinboard
- Hold *ctrl* while selecting a bookmark to mark or unmark it
- Hold *shift* while selecting to send URL to pocket. You need to set auth_token using
  **pbauthpocket**
