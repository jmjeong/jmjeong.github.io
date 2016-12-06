---
layout: single
title: HappyDays/Download
description: 
category: [palm, happydays]
tags: palm palmprogram
---

#### File Download  

* [happydays-3.01.zip](https://dl.dropboxusercontent.com/u/4345768/jmjeong.com/happydays-3.zip) -- English version 
* [happydays-src-3.01.zip](https://dl.dropboxusercontent.com/u/4345768/jmjeong.com/happydays-src.zip) -- Source file, [Handera 330 SDK](https://dl.dropboxusercontent.com/u/4345768/jmjeong.com/handera-sdkv105.zip)
* [Github Link](https://github.com/jmjeong/happydays.palm)

If you use the Happydays 1.x version, you **should** uninstall the old version due to HappyDaysDB
name change before you install the new version. **In Happydays 3.x version, you should install
lunarlib.prc file together.**

- Refer [HappyDays Page]({% post_url 2004-03-08-HappyDays %})


#### Localizations 

If you would like to translate HappyDays into your favorite language, please mail me and let me
know. To translate HappyDays into your favorite language, you need to copy 'translate/english.msg'
file into xxx.msg and edit xxx.msg file. Translate the right part( i.e. the phase after '=') into
your favorite language. See the sample english.msg file.(It is just sample file. If you want to do
the localization, download the source file and refer translate/english.msg file.)

You can download the localized version from [link](https://www.dropbox.com/home/Public/jmjeong.com/HappyDays)

HappyDays has been translated into the following languages: 

- Korean(3.01) - by Jaemok Jeong, (happydays-k8.prc for 8x8 font) 
- German 
	  -  German(2.37) - by Gunther Zagatta (zagatta at web.de) 
	  -  German(3.01) - by Martin Klinkigt (klinkigt at googlemail.com)
- Spanish
	  -  Spanish(2.1 beta1) - by Juan Fernando Calder&oacute;n (jfcalderon at dominium.com.mx) and Manuel Tornos(palm at povisa.es) 
	  -  Spanish(2.37) - by Alejandro Lizarraga(bow2axel at hotmail.com)
-  Catalan(2.37) - by [PalmCat.org](http://www.palmcat.org) 
-  Portuguese Brazilian (2.08 beta1) - by Mauricio Montel (maumontel at hotmail.com) 
-  Chinese(2.29) - by Daitau Aaron(daitau at hotmail.com)  - (happydays-chi-gb.prc for GB Encoding, happydays-chi-big5.prc for Big5 encoding) 
-  Norwegian(2.08 beta2) - by Knut Zakariassen (palmos at zakariassen.net) 
-  Czech(2.08 beta1) - by Petr 'PePa' Pavel (petr.pavel at quick.cz) 
-  Turkish(2.08) - by Engin Utkan (engin.utkan at usa.net) 
-  Italian(2.08) - by Andrea Monteriu' (monteriu at tin.it) 
-  French
	  -  French(2.08 beta 2) - by Cyril-Vianney BEKIER (cyril at bekier.org)
	  -  French(3.01) - by Antoine(websearch at wanadoo.fr), [HomePage](http://www.freewarefrance.com/)
-  Russian(2.07 beta 1) - by Alexander (spirit at reactor.ru) 
-  Thai(2.37) - by Kaptan Teotrakool(kteotrakool at hotmail.com) - Requires Thai Language Hack (ThaiPOS or ThaiHack) 
-  Dutch(1.45) - by Roy Huijts 

#### Change log  

- Happdyays 3.01 version - (2007-11-06)
	- Fix a minor bug, the drop down list "noti fmt" saves it state regardless of whether the save or cancel button is selected
- Happydays 3.0 version - (2007-07-24)
	 -  New PIMS DB Support such as Calendar, Contacts, Todos, and Memos
	    - Support the additional fields of Contacts; from custom 5 to custom 8
	    - Support the built-in birthday field of Contacts
	    - Fix the compatibility issue between Happydays and New PIMS DB
	 - Support the customizable notification format
	 - Separate the lunar calculation routine into the shared library 
- Happydays 2.37 version - (2005-05-13)
	- (Fix) Error in lunar date chck routine of 2.36
-  Happydays 2.36 version - (2005-05-09)
	- (Fix) Error in date parsing routine
- Happydays 2.35 version - (2005-05-09)
	- (Fix) Wrong lunar date calculation(missing 2006.1.30 in lunar)
-  Happydays 2.34 version - (2004-11-23)
	- (Fix) Fix Wrong lunar date calculation(2006.1.1 in lunar)
	- (Change) Enhance checking wrong lunar date while reading address book
- Happydays 2.33 version - (2004-05-07)
	- (Add) Support for Sony Clie Hires+
- Happydays 2.32 version - (2004-04-20)
	- (Add) Datebook category support in Date Book Notify
	- (Change) You can edit category of Datebook or Todo in HappyDays notify screen.
- Happydays 2.31 version - (2004-03-08)
	- (Add) Can Assign N-th day of Event.
- Happydays 2.30 version
	- (Add) Give different icon or color to different event types. You can set any note field for each event type with "= HappyDays Notes". 
	- (Enhance) Change the color for table select
- Happydays 2.29 version - (2004-01-03)
	- (Fix) Error in lunar calculation(2004-9-30)
-  Happydays 2.28 version - 2003-04-27
	- (Enhance) Enhance age sort - within same age, sort the age not name
- Happydays 2.27 verision - 2003-04-21
	- (Add) Add HanAD(http://bliss.hanirc.org/HanAD/\.) as Addressbook replacement
	- (Enhance) Preference screen
- Happydays 2.26 version - 2003-03-10
	- (Fix) Memory allocation error  which was added in 2.25
- Happydays 2.25 version - 2003-03-07
	- (Add) Notify format '\[First] E(1) Year'
- Happydays 2.24 version - 2003-01-16
	- (Fix) the problem of freezing after datebook notify in some device such as m505/515(added in 2.22 version)
- Happydays 2.23 version - 2003-01-15
	- (Fix) Find function will cause Fatal error(added in 2.22 version)
- Happydays 2.22 version - 2003-01-14 
	- (Fix) Fix a bug of alarm function in datebook notify
- Happydays 2.21 version - 11/27/2002 
	- Palm OS 5 compatible 
	- Fix repeated 'please run datebook once' error 
	- Increase note field size from 25 to 125 
	- 'Custom field' of Address is now optional 
	- Address.kr is removed from Goto menu 
	- Some tweaks 
- Happydays 2.12 version - 4/23/2002 
	- Fix memory leaks in Datebook Notify 
	- Fix a compabibility issue on Palm OS 3.3 
	- Change Datebook Notify - To show age in each record, Happydays makes individual entries rather than repeating entry, if 'repeat for' setting is more than 1 
	- Add a general Note field in ToDo Notify 
- Happydays 2.1 version - 4/21/2002 
	-  Add a general note field in DateBook Notify for Action Names, DateBk3/4, and old icon stuff is removed.
	- Now you can add category, font, and icon information of Action Names, DateBk3/4 in Datebook Notify. Refer ** Action Names, DateBk3/4 manual for more information. 
	- Add the option : Ignore record with prefix '!'
	- You can put `!' before the entry of a happydays field in Address book. This record can be hidden in Happydays with check option. 
	- Date parsing routine is changed. 
	- Year number between 0 and 31 is used for the year 2000-2031, and Year number between 32 and 99 is used for the year 1932-1999. 
- Happydays 2.08 version - 2/3/2002 
	- Add a scan process widget in start screen. 
	- Fix a bug : If the value in 'repeat for' entry is too large, invalid record is created. 
	- Change Export to memo format : for lunar entry, incoming event date is recorded also. 
- HappyDays 2.07 version - 9/21/2001 
	- Add calendar in HappyDays View screen in the case of Handera 330. 
	- Some modification 
-  HappyDays 2.06 version - 7/25/2001 
	-  Fix the bug which makes Palm crash if one try to edit the erroneous note field(Reported by Hendrik and Jeff). 
	- Fix a bug : When the entry is notified into DateBook or ToDo, the entry in lunar is not affected by 'Look up' Selector(Reported by Inyeol Lee). 
-  HappyDays 2.05 version - 6/29/2001 
	- Fix a bug in Age calculation routine. 
- HappyDays 2.04 version - 6/22/2001 
	- Fix a bug in global find 
	- Fix a bug in 'Instead of system date format' option 
	- Fix a bug in date difference calculation 
- HappyDays 2.0 version - 6/20/2001 
	- Full support for Handera 330 with 240 x 320 screen resolution with virtual graffiti area, while running properly on the "normal" Palm-powered devices with 160x160 screen. 
	- Support for Jog dial 
	-  Change HappyDays list screen such as scroll bar and button 
	-  Refine HappyDays view screen 
	-  Color icon has the transparent background 
	-  Change HappyDaysDB name 
	-  Font selection in HappyDays list 
	-  Add 'Address Autoscan' option. 
	- And more 
