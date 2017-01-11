---
layout: post
title: HappyDays/Manual
description: 
category: [palm, happydays]
tags:  palm
---

## Introduction  

HappyDays is a program for Palm hand-held computers. It helps you to remember the birthdays or anniversaries of your friends and family. It gathers information from the built-in AddressBook application and exports notification record into the built-in Datebook, To Do or Memo Pad application. It supports the same categories as defined in the AddressBook.

- Refer [HappyDays Page]({% post_url 2004-03-08-HappyDays %})
- [Korean Manual](http://www.114pda.com/personal/live/happydays.htm)

## Installing HappyDays  

- Obtain the HappyDays distribution file(you've probably done this already, since you're reading this manual)  
- Extract the distribution file (a .ZIP archive) into the directory you wish to keep the files in. You don't need to keep the extracted files after the installation, but you may wish to keep them so as to have the Manual available to you in the future. 
- Install the happydays.prc file into your Palm OS device 

## Upgrading HappyDays  

If you have used HappyDays 1.x version, delete the old version before you install the new version. 

## Quick start  

If you run happydays for the first time and you have never executed Datebook, you could encounter the following screen. Then just run Date Book once first.
 
HappyDays gather the event information from Address Book, and notify it into Date Book, To Do, and Memo. For entering and modifying the events you'll use the Address Book.

![](http://farm3.staticflickr.com/2765/13211895233_aa35e10b9b_o.png)

Start the Address Book application, use the menu key and select 'Options/Rename Custom Fields...'. (**This is Address Book application.**)

![](http://farm4.staticflickr.com/3772/13211747895_2fbdbbf4d2_o.png)

You should now rename any of the custom field to 'Birthday'. HappyDays use only one of custom field for many event types. The default name for the custom field looking for HappyDays is 'Birthday'. You can change this value in Preferences in HappyDays. (**This is Address Book program**)

![](http://farm4.staticflickr.com/3728/13211753545_1414e3f132_o.png)

Now you can enter the event information using the Address Book application. Use the birthday field to enter the day of the person.

![](http://farm4.staticflickr.com/3766/13212085244_4a9cdb7d45_o.png)

Date format for input is determined by 'System/Prefs/Formats/Date Format'.(**This is Prefs program**) If you want to use the different date format, you could change it in preferences of HappyDays. 

![](http://farm4.staticflickr.com/3763/13211997565_6a26903a6d_o.png)

Then now run HappyDays application, you can see this screen.

![](http://farm4.staticflickr.com/3683/13212384324_9836d232ef_o.png)

If you use the wrong input date to enter the day of the person, you will encounter this screen when you start happydays. 'Enter' button is used for modifying the error record, 'Ignore' is used for ignoring this one record, 'Ignore all' is used for ignoring the following error record.  

![](http://farm3.staticflickr.com/2851/13212215933_499849e0ec_o.png)

This screen shows how to enter multiple event in a single Address Book record. Last name for the birthdays entered on several lines will be taken from the Address record itself. The Firstnames have to be entered as part of each line in the format shown in the example on the screen. Each line starts with an asterisk '*', followed by a space ' ', followed by the Firstname(which may contain anything but a space-character, if you want to enter space-character, use '_'), followed by another space ' ' and then followed by the Birthday in the format that you specified in the preferences.  If you don't want to display Lastname, add a dot('.') before the Firstname field in custom field.

## Manual

### Main Screen of HappyDays 

![](http://farm4.staticflickr.com/3790/13212402804_e84c26c420_o.png)

This is HappyDays list view. All information gathered from Address Book is displayed in this
screen. You can traverse the past or future event using Look up Trigger located at bottom. If you
tab 'N' button, HappyDays is sorted using Name field. If you tab 'D' button, HappyDays is sorted
using incoming date field. If you tab 'A' button, HappyDays is sorted using age field. If you tab
'A' button twice, sort order is changed and you can view list in descending order.

![](http://farm4.staticflickr.com/3798/13212228453_bb44309881_o.png)
  
- Font - Select font for HappyDays list 
- Preferences - HappyDays Preferences 
- Display Preferences - HappyDays Display Preferences 
- About HappyDays 

![](http://farm4.staticflickr.com/3725/13212084465_d0b5695038_o.png)
 
* Date Book Notify - for Date Book notification 
* Cleanup Date Book - Erase the notified record from Date Book 
* To Do Notify - for To Do notification 
* Cleanup To Do - Erase the notified record from To Do 
* Export to Memo Pad - Export HappyDays list into Memo Pad 
* Solar to Lunar - Utility for converting the Julian(solar) to Lunar calendar 
* Lunar to Solar - Utility for converting the Lunar into Julian(solar) calendar 
* Rescan Address Book - Force HappyDays to rescan Address Book. It is useful if you set 'Address Autoscan' to Never. 

 
### Preferences  

"HappyDays preferences" are global application behavior settings, which is to say as part of the
program configuration. "Display Preferences" are also global and applied to screen but is focused on
customizing the HappyDays display.

#### 1. HappyDays Preferences 
.
![](http://farm4.staticflickr.com/3801/13212100255_7d70fba712_o.gif)
. 
##### 1.  Custom field : Specify the name of custom field in Address Book used for HappyDays.

  *Defaults: Birthday; If use doesn't specify the event type, this name is used for default event type.*

##### 2. Instead of system date format Use ...

If you want to use the different date format from system date format in HappyDays, check this option and select the preferred date format. 
*Defaults: off*

##### 3. Scan note field

If this check box is on, HappyDays scans not only custom field but also note field of Address
Book. For information about entering the data in note field, refer Data input format.

*Default: Off; it isn't needed by a lot of people*

##### 4. Ignore note with prefix '!'

If you check this option on, happydays record with prefix '!' is ignored. *Default: on;*

##### 5. Address autoscan

When Address Book change is detected, HappyDays automatically rescan Address Book. You can specify whether this option will be on or off.
*Default: Always;*

- 'Always' - always rescan AddressDB 
-  'Ask' - Ask user if you want to rescan AddressDB. 
- 'None' - never rescan AddressDB. You can force HappyDays to rescan AddressDB using 'Rescan Address Book' menu.

##### 6. Notify format:

When you notify event information into built-in Date Book or To Do application, this format is used
to generate notify string. 'Last' means by LastName, 'First' means by FirstName, 'E(1)' means by the
first character of Event type string, 'Event' means by Event type string, and 'Year' means by source
year of event. If you set 'Repeat for' to 1 in Date Book Notify, 'Year' is changed into Age.

- [Last, First] E(1) Year : [Jeong, Jaemok] B 30
  This format is preferable for ActionNames. ActionNames treats automatically the name between '[' and ']' as Contact information. 
- [First Last] E(1) Year : [Jaemok Jeong] B 30\n
  This format is preferable for ActionNames. ActionNames treats automatically the name between '[' and ']' as Contact information. 
- Event - Last, First Year : Birthday - Jeong, Jaemok 30\n
  This format is preferable for built-in Date Book or DateBk3/4. 
- Event - First Last Year : Birthday - Jaemok Jeong 30\n
  This format is preferable for built-in Date Book or DateBk3/4. 
- First Last Year : Jaemok Jeong 30\n
  This format is preferable for built-in Date Book or DateBk3/4.
  *Default: [First Last] E(1) Year;* I use ActionNames, and this notify string is preferable to ActionNames. :-)
  
##### 7. Address Book:

Specify the Address Book program where you jumps, when you select 'Goto' button in HappyDays View.
*Default: Builtin Address Book*
. 
#### 2. Date Book Notify
.
![](http://farm4.staticflickr.com/3813/13212340643_4843f3819f_o.png)
.
##### 1. Records

If you select 'Date Book Notify' in menu, you can see only 'all' button. If you jump to this screen
using 'DB' button in View screen, you can select 'all' or 'selected' button. 'all' means that all
happydays entries in the selected category will be notified into Date Book. 'selected' means that
selected happydays entries will be notified into Date Book.

##### 2. Existing

'keep' means that the the existing notify entry in Date Book will not touched. 'modify' means that
the existing notify entry in Date Book will be modified. *Defaults: keep;* 'keep' option can
speed up notify action.

##### 3. Category

Specify the category where the notified Datebook record is contained. Some Datebook replacement
program such as WP+, Agendus, and Datebk5 support Datebook's category. *Default: Unfiled*

##### 4. Private

If this option is checked, the record created in Date Book will be private.
*Defaults: off;* I have no secret. :-)

##### 5. Alarm

This option will set the alarm notification in your Date Book entry. Set the number of days in advance you'd like to get notified.
*Defaults: 3 Days*

##### 6. Time

Specify the time field of the notified record. Usually used with 'Alarm' together.
*Defaults: No time*

##### 7. Repeat for

This option specifies how many years the event will be notified. If you set 'Repeat for' to 1, you can see 'Age' in the description of the notified record .

-1 means repeat forever in case of solar date event, and means repeat for five years in case of lunar date event.

*Defaults: 1 year;* I want to to see 'age' in the description of the notified record. *Changed in 2.1 version*.

#### 3. DateBook(Todo) Icon

![](http://farm4.staticflickr.com/3812/13212231775_ce66ca0c16_o.png)
![](http://farm4.staticflickr.com/3806/13212383083_b0bb45acdd_o.gif)
.
##### 1. Icon support(Before 2.0x version)

If you use the Date Book replacement program such as Action Names or DateBk3/4, you can specify the icon in the notified record. If you want to set icon in record, use this screen. For AN Icon Number, consult Action Names manual. But there is easy way to know the AN icon number for AN events. Make the NEW MEETING with the appropriate icon in ActionNames Datebook. And open the built-in Date Book
and look up the created event. You can see the AN icon number in the note field of the searched record. DateBk3/4 Icon is read from MemoPad. If you don't have DateBk3 Icon entry in MemoPad, nothing is displayed. *Defaults: off*

##### 2. Datebook Note(After 2.1 version)

To give more flexibility to user, the form of 'datebook icon' is changed into the form of 'datebook note'. You can set the arbitrary note content in this field. In Datebk3/4 or ActionNames, note field is used for representing icon, font, and category etc. You could refer their manual to know the exact syntax to be entered.  


##### 3. Give different icon or color to the different event type

The feature of Datebook Note explained in the previous item has a drawback. You can set one note field for Datebook(Todo) notification. Naturally, you can change the datebook note whenever you perform 'Datebook notify', but it is cumbersome. So Happydays 2.30 version support the predefined note string for each event type.

In MemoPad, make '= HappyDays Notes' note. In this memo, you can predefined note string for each event type. If 'Add the following note' check box is off, the predefined note string is used during notifying to Datebook or Todo. Agendus or Datebook use the note string for describing color or icon.

    = HappyDays Notes
    * Birthday
    ICON: 24
    #AN
    * Wedding
    ICON: 236
    #AN


#### 4. To Do Notify

![](http://farm3.staticflickr.com/2716/13212579864_a28f0712d7_o.png).
.
###### 1. Records

If you select 'To Do Notify' in menu, you can see only 'all' button. If you jump to this screen using 'TD' button in View screen, you can select 'all' or 'selected' button.

'all' means that all happydays entries in the selected category will be notified into builtin ToDo application. 'selected' means that selected happydays entries will be notified into ToDo application.

##### 2. Existing
Same as 'Existing' option in 'Date Book Notify'. *Default: keep*

##### 3. Priority

Specify the priority of the notified ToDo record. *Default: 1*

##### 4. Category

Specify the category where the notified ToDo record is contained. *Default: Unfiled*

##### 5. Private

If this option is checked, the record created in ToDo will be private. *Default: off* 

## Input Data format of HappyDays  

### Introduction

This data format is used when you input information in the custom field or note field in Address Book. The date format is automatically read from the system preferences.If you input the information in wrong date format, you will encounter 'Invalid event format' error message. If the first entry in this field starts with a digit, HappyDays will read this information. An example is:

    12/31/1970

You can omit the year field. If you are not sure of the year format, just write it in form of YYYY(e.g. 1970). Year must be in 1904 and 2301, because HappyDays use the built-in date type of Palm OS for reducing DB size. Year number between 33 and 99 is assumed to be year in 20th century, and year number between 00-31 is assumed to be year in 21th century.(Changed in 2.1 version)

If you want to input lunar date information, prepend '-)' or '#)' before date. '-)' means by date according to the lunar calendar, and '#)' means by the lunar leap month according to the lunar calendar.

If you checked "Scan addr notes" in your Preferences settings, HappyDays will look for events in the notes attached to your Address Book records, too. This was intended to support multiple lines for a whole family and multiple types of events. There is no reason why the custom field shouldn't contain multiple lines, too. So both the notes field and the custom-field are checked for multiple lines in the event Format described further below.

    [*[{EventType}]\\ws{Description}] {Date}[nth day list]

* \\ws means by white space(space, tab etc).
* If EventType is omitted, Renamed custom field is used for default EventType.
* If Description is omitted, Last name and First name of Address book entry is used.
* Date format for input is determined by 'System/Prefs/Formats/Date Format'. You can change it in Prefs screen.
* If you want to calculate n-th day since Event, you can set '''nth day list'''; Each nth day is separated by ','(Max number of nth day is 20).\n
For example) *Wedding Jaemok 11/23/2004[100,200,300]

### Examples

When 'System/Prefs/Formats/Date' is 'Y/M/D'. 

      1980/1/31        Jan, 31, 1980(the solar calendar)
      5/30             May, 30(the solar calendar)
      -)1970/12/4      Dec. 4, 1970(the lunar calendar)


When Date format is 'D.M.Y' 


      31.1.80          Jan, 31, 1980(the solar calendar)
      30.5 or 30.5.    May, 31(the solar calendar)
      Format of Event entries


HappyDays expects a multi-line entry of a custom field or a note to look like: 


    * Jaemok 12/31/1970
    * Sumiae 1/1/1945
    *Wedding Mother&Father 3/23/1940


Each event in the note or field should be on a separate line. The lines need to start with a "*" to be recognized by HappyDays. Each line consists of three fields which should be delimited by one or more blanks.


    First field: Type of event ("*" for default event) 
    Second field: Name of Person/event (e.g. Jaemok)
    Third field: Initial Date of event (e.g. 12/31/1970)


There may be no extra blanks in each field! So the type of event needs to go directly with the first "*", (e.g. "*Wedding", "*Holiday") If the name of the person or event consists of more than one word, use an underscore(e.g. "Grand_father"). Underscore is automatically interpreted into space ' '. If you don't want to display a last name, add a dot('.') before the event name.

The record with prefix '!' could be ignored or read in Happydays depending on preference setting. It could be useful to record, which is not frequently looked up.

#### Examples - Anniversaries

If you want to register anniversary such as NewYear or ThanksgivingLunar, you can insert this data in one AddressBook entry. For your information, Lunar date is changed every year.

    Last name: Anniversary
    ...
    ...
    Birthday: * New_Years_Day 1/1
    * New_Years_Lunar -)1/1
    *Event Father's_Day 8/2
    * .Thanksgiving_Lunar -)8/15
    ...

In HappyDays list view, you can see the following.

    ...
    Anniversary,New Years Day        00/1/1  -B
    Anniversary,New Years Lunar      00/2/5  -B
    Anniversary,Father's Day         00/8/2  -E
    Thanksgiving Lunar               00/9/12 -B
    ...


In this screen, '-' means that HappyDays couldn't calculate the age of the event, because the year is not provided. The last char 'B' is the initial of the event type. In this example, 'B' means 'Birthday', the default event type. 'E' means 'Event'. If you don't want to display a last name, add a dot('.') before the event name.

#### Using note field of Address Book for input data

In the preferences menu, there is 'Scan from note field' control. Check this check box and HappyDays will search the note field in address book. Because note field in address book is sometimes used to keep another information, HappyDays searches the only region from HappyDays identifier(which is '*HD:' string) to another HappyDays identifier or end of notes. That is, HappyDays stop scanning on seeing the end marker or end of notes(whichever comes first).


	[NOTE FIELD]

	Other information....
	...
	..

	*HD:        
	1/2                    -|
	*Birthday Jane    4/30  +-  Data region
	*Wedding Ann&Gary 1/1  -|
	*HD:

	..
	...
	Another information....


### Some useful tips  

* Name1 & name2 displayed in HappyDays List is determined by 'AddressBook/Preferences/List by'. If you change this preferences, you can see the different views. 
* You can see the sorted view by tapping on 'D,N,A' button in bottom of HappyDays screen. If you tap 'A' button again, age sorting order is changed into ascending/descending order. 
* If you write character or number in graffiti area, the matching row is highlighted. For example, if you write 'a' in graffiti, the first record beginning with 'a' or 'A' is highlighted. If you write '1' in graffiti, the nearest incoming record after January is highlighted. 
* In case of Solar event, Date field is omitted, because the date field is redundant. Since the entry is made on *that* day already, this text is kind of superfluous. For lunar event, Date field is displayed because the actual solar day is changed every year. And 'AGE' is displayed if possible. If entry date doesn't have year field or repeating is set for solar event, this field is omitted. If you want to see 'AGE' field, set 'repeat for' to 1. 
* You can look up the past or future event using 'Lookup' selector. 
* In 'HappyDays View' screen, you can move the previous/next record using hardware up/down button. And you could use Jog dial to traverse record 


