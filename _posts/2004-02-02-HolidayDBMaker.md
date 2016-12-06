---
layout: single
title: HolidayDBMaker
description: 
category: palm
tags:  palm palmprogram 
---

### HolidayDBMaker

HolidayDB.pdb Generator. Currently WP+, WeeklyPlan, and MonthPlanner use HolidayDB.pdb.

- Download : [HDMaker (Version 1.3)](https://dl.dropboxusercontent.com/u/4345768/jmjeong.com/HDMaker.zip)

### How to input Holiday

#### General Rules 

- All lines staring with ';' are comment, You can add comment with ';' in any places of lines
- Descrition string for Datebook notify is started with ':'. It is used for Datebook Notify
- Starting lines with '*' are ignored during 'Create HolidayDB'.
- Each entry is divided with '\\n'. You can enter one holiday entry in one line.
- You can specify the duration such as the day after or before holiday with '\[' and '\]'
  - ex) 1/1\[-1,0,1] ; A Day before New year, New Year, A Day after New Year.
- If year field is specified, it only occurs on that year. Or it is repeated on the years specified in Prefs.

#### Input Format 

##### Fixed Day(like New Year's Day, Christmas Day, Halloween)

It follows the system date format. If Date Format is 'M/D/Y', you can input '10/2/2004'.  You can
input lunar date with -) and #). -) means by lunar day, and #) means by lunar leap day.

	* Examples
	** 1/1 : New Year
	** 10/31 : Halloween
	** 12/25 : Christmas 
	
	** -)8/15[-1,0,1] : Chuseok in Korea
	** -)1/1[-1,0,1] : Seol in Korea

##### Day of Month(Example: First Sunday of June; like Daylight Saving's Start/End, Martin Luther King's Day)


	@c(month, week_of_month, day_of_week)
	@c(month, week_of_month, day_of_week, year)


If `week_of_month` is -1, it means by the last week. `day_of_week` must be between 0 and 6(Sun=0, ..., Sat=6).

	* Examples
	** @c(2, 3, 1) : President's Day Observed(Third Monday in February)
	** @c(9, 1, 1) : Labor Day Observed(First Monday in September)
	** @c(10, 2, 1) : Columbus Day Observed(Second Monday in October)

##### Easter related(x days before Easter Sunday; Like Easter Sunday)

	@easter
	@easter(year)

	** @easter(2004) : Easter Sunday in 2004
	** @easter[-4] : Four days before Easter Sunday

---


HolidayDB is the Palm date file, which contains Holiday Information. Currently WeeklyPlan and
PalmWiki:MonthPlanner use this information. You can generate HolidayDB by HolidayDBMaker.

### Data structure of HolidayDB.pdb(Creator: Holi, Type: DATA)

Each record has Holiday information.  To speed up the check of Holiday, every recurring holiday is
stored as the separate entry. HolidayDB is sorted by asending order with date.

### Record Structure 

```c
typedef struct {
   UInt16 year :7 ; //years since 1904 (Mac format)
   UInt16 month :4;
   UInt16 day :5;
} DateType;
```

### If you want to use HolidayDb in your program...

####  HolidayDB Open

```c
    HolidayDB = DmOpenDatabaseByTypeCreator('DATA', 'Holi', mode);
```

#### HolidayDB Close

```c
    if (HolidayDB) DmCloseDatabase(HolidayDB);
```

#### Check Holiday 

-  Boolean IsHoliday(DateType date) - Return true if the date is holiday

```c
static Int16 DateCompare(DateType d1, DateType d2)
{
    UInt16 int1, int2;

    int1 = DateToInt(d1);
    int2 = DateToInt(d2);

    if (int1 > int2)
        return (1);
    else if (int1 < int2)
        return (-1);
    return 0;
}

static Int16 DateCompareRecords(DateType *rec1,
                                DateType *rec2,
                                Int16,
                                SortRecordInfoPtr,
                                SortRecordInfoPtr,
                                MemHandle)
{
    extern Int16 DateCompare (DateType d1, DateType d2);
    
    return DateCompare(*rec1, *rec2);
}

Boolean IsHoliday(DateType date)
{
    extern Int16 DateCompare (DateType d1, DateType d2);
    extern DmOpenRef HolidayDB;
    UInt16  index;
    MemHandle   recordH;
    DateType *ptr;

    if (!HolidayDB) return 0;
    
    index = DmFindSortPosition(HolidayDB, &date, NULL, (DmComparF*)DateCompareRecords, 0);
    if (index > 0) {
        recordH = DmQueryRecord(HolidayDB, index - 1);
        if (recordH) {
            ptr = MemHandleLock (recordH);
            if (DateCompare(*ptr, date) == 0) {
                MemHandleUnlock(recordH);
                return -1;
            }
            else {
                MemHandleUnlock(recordH);
                return 0;
            }
        }
    }

    return 0;
}
```
