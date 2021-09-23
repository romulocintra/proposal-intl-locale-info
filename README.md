# Intl Locale Info API

## Draft Spec
https://tc39.github.io/proposal-intl-locale-info 
## Stage 
Stage 3

* Advanced to [Stage 1](https://docs.google.com/presentation/d/1NwYFb6jm5aQOiL9urMM-GaEFMhll5sYcZJYQ1WZhTZ8/edit#slide=id.p) in TC39 2020-09 meeting.
* Advanced to [Stage 2](https://docs.google.com/presentation/d/1ct7h9pLHmXCwojGlReNjAT9RgysqLk_3lyUcllnOQYs/) in [TC39 2021-01-25~28 meeting](https://github.com/tc39/agendas/blob/master/2021/01.md).
  * Jan 2021 TC39 meeting approve to move to Stage 2 **WITH the condition to drop unitInfo**
* 2021-04-08 ECMA402 meeting, we agreed to propose to TC39 for Stage 3.
* Advanced to [advance to Stage 3](https://docs.google.com/presentation/d/1h-iaDM5RiD5rpb0aYr1GMRLRRBh72zVEKtMyMJkCkfE/edit#slide=id.g98718d9573_0_37) in [TC39 2021-04 meeting](https://github.com/tc39/agendas/blob/master/2021/04.md).
* [Update during Stage 3](https://docs.google.com/presentation/d/1rrEaInlUFpYJ3djkRfQHpMBzt0C88WuQeFGis8x9UP8/edit#slide=id.p) in [TC39 2021-07 meeting](https://github.com/tc39/agendas/blob/master/2021/07.md).

### Entrance Criteria for Stage 1 (Proposal)
* Identified “champion” who will advance the addition: **Frank Yung-Fong Tang**
* Prose outlining the problem or need and the general shape of a solution: **See this document**
* Illustrative examples of usage: **See this document**
* High-level API: **See this document**
* Discussion of key algorithms, abstractions and semantics
* Identification of potential “cross-cutting” concerns and implementation challenges/complexity
* A publicly available repository for the proposal that captures the above requirements:

### Entrance Criteria for Stage 2 (Draft)
* Above
* Initial spec text: DONE
* **Acceptance Signifies**: The committee expects the feature to be developed and eventually included in the standard

### Entrance Criteria for Stage 3 (Candidate)
* Above
* Complete spec text
* Designated reviewers have signed off on the current spec text
* All ECMAScript editors have signed off on the current spec text
* **Acceptance Signifies**: The solution is complete and no further work is possible without implementation experience, significant usage and external feedback.


## Champion
* Frank Tang @FrankYFTang

## Designated reviewers
* Shane Carr @sffc
* Zibi Braniecki @zbraniecki 

## ECMAScript editors
* Richard Gibson @gibson042 

## Implementation Status

* V8 (**UPDATE 2021-5-6:**) : Behind a flag ([cl/2570218](https://chromium-review.googlesource.com/c/v8/v8/+/2570218) is landed into the trunk) 
  * $ out/x64.release/d8 --harmony_intl_locale_info
  * Chrome - [TBD](https://www.chromestatus.com/feature/5566859262820352)
  * Edge - ???
* FireFox - [Tracking Bug](https://bugzilla.mozilla.org/show_bug.cgi?id=1693576)
* Safari - ???

## Scope

A proposal to expose Locale information, such as week data (first day in a week, weekend start day, weekend end  day, minimum day in the first week), and text direction hour cycle used in the locale ~,measurement system used in the locale~.

* Week Data: (User request: https://github.com/tc39/ecma402/issues/6 )
  * Prior Arts: 
    * [weekstart](https://github.com/gamtiq/weekstart) JS Library to get first day of week. getWeekStartByRegion(RegionCode) / getWeekStartByLocale(locale);
    * [mozIntl.getCalendarInfo( locale )](https://firefox-source-docs.mozilla.org/intl/dataintl.html#mozintl-getcalendarinfo-locale)
    * ["date-fns/is_weekend" an non-i18n weekend javascript library](https://date-fns.org/v1.9.0/docs/isWeekend)
    * ['date-fns/start_of_week' an non-i18n weekend javascript library](https://date-fns.org/v1.29.0/docs/startOfWeek)
    * [JS code snippet of non-i18n solution on stackoverflow](https://stackoverflow.com/questions/3551795/how-to-determine-if-date-is-weekend-in-javascript)
    * ICU4J [Calendar.getWeekData()](https://unicode-org.github.io/icu-docs/apidoc/released/icu4j/com/ibm/icu/util/Calendar.html#getWeekData--) and [Calendar.WeekData](https://unicode-org.github.io/icu-docs/apidoc/released/icu4j/com/ibm/icu/util/Calendar.WeekData.html#minimalDaysInFirstWeek)
    * ICU [Calendar](https://unicode-org.github.io/icu-docs/apidoc/released/icu4c/classicu_1_1Calendar.html)
      * [Calendar::getFirstDayOfWeek](https://unicode-org.github.io/icu-docs/apidoc/released/icu4c/classicu_1_1Calendar.html#aa95d4e17ea169d0388a3a18489e67da0)
      * [Calendar::getMinimalDaysInFirstWeek](https://unicode-org.github.io/icu-docs/apidoc/released/icu4c/classicu_1_1Calendar.html#af10922ea91e4e4ccef6624ac3f18e621)
      * [Calendar::getDayOfWeekType](https://unicode-org.github.io/icu-docs/apidoc/released/icu4c/classicu_1_1Calendar.html#adc18b432f868737e115ece5f6e3c95ab)
* ~Hour Cycle~ DROPPED by Champion
* Direction (User request: https://github.com/tc39/ecma402/issues/205 )
  * Prior Arts: 
    * [mozIntl.getLocaleInfo(locales, options)](https://firefox-source-docs.mozilla.org/intl/dataintl.html#mozintl-getlocaleinfo-locales-options)
    * [Closure goog.i18n.bidi.isRtlLanguage(language)](https://github.com/google/closure-library/blob/master/closure/goog/i18n/bidi.js)
    * [rtl-detect](https://www.npmjs.com/package/rtl-detect)
* ~Measurement System:~
  * ~Prior Arts:~
    * ~ICU4J [LocaleData.getMeasurementSystem](https://unicode-org.github.io/icu-docs/apidoc/released/icu4j/com/ibm/icu/util/LocaleData.html#getMeasurementSystem-com.ibm.icu.util.ULocale-) and [LocaleData.MeasurementSystem](https://unicode-org.github.io/icu-docs/apidoc/released/icu4j/com/ibm/icu/util/LocaleData.MeasurementSystem.html)~
    * ~ICU4C [ulocdata_getMeasurementSystem](https://unicode-org.github.io/icu-docs/apidoc/released/icu4c/ulocdata_8h.html#a7abb69df19b1080b76fcc26ec0ea0978)~

## Motivation / Use Case

Locale Information is necessary for many low level operations.

* Direction in textInfo will be needed for layout, and for localization information (bidi boundaries with placeholders etc.)
* WeekInfo will be needed for calendar widgets and applications to display correct monthly and weekly views.

## High Level Design


Add methods to Intl to get object to contains group of information:
#### Week Data

```js
let he = new Intl.Locale("he")
he.weekInfo
// {firstDay: 7, weekend: [5, 6], minimalDays: 1}
let af = new Intl.Locale("af")
af.weekInfo
// {firstDay: 7, weekend: [6, 7], minimalDays: 1}
enGB = new Intl.Locale("en-GB")
enGB.weekInfo
// {firstDay: 1, weekend: [6, 7], minimalDays: 4}

let msBN = new Intl.Locale("ms-BN")
msBN.weekInfo
// {firstDay: 7, weekend: [5, 7], minimalDays: 1}  // Brunei weekend is Friday and Sunday but not Saturday 
```
Monday is 1 and Sunday is 7, as defined by ISO-8861 and followed by [Temporal proposal](https://tc39.es/proposal-temporal/#sec-temporal-todayofweek)
#### Text Information
```js
l = new Intl.Locale("ar")
let textInfo = l.textInfo;
// { direction: "ltr" }
l.textInfo.direction
// ltr
```

#### Defaults
```js
~/v8/v8$ out/x64.release/d8 --harmony_intl_locale_info
V8 version 9.1.0 (candidate)
d8> ar = new Intl.Locale("ar")
ar
d8> ar.calendars
["gregory", "coptic", "islamic", "islamic-civil", "islamic-tbla"]
d8> ar.collations
["compat", "emoji", "eor"]
d8> ar.hourCycles
["h12"]
d8> ar.numberingSystems
["latn"]
d8> ar.timeZones
undefined

d8> arEG = new Intl.Locale("ar-EG")
ar-EG
d8> arEG.calendars
["gregory", "coptic", "islamic", "islamic-civil", "islamic-tbla"]
d8> arEG.collations
["compat", "emoji", "eor"]
d8> arEG.hourCycles
["h12"]
d8> arEG.numberingSystems
["arab"]
d8> arEG.timeZones
["Africa/Cairo"]

d8> arSA = new Intl.Locale("ar-SA")
ar-SA
d8> arSA.calendars
["islamic-umalqura", "gregory", "islamic", "islamic-rgsa"]
d8> arSA.collations
["compat", "emoji", "eor"]
d8> arSA.hourCycles
["h12"]
d8> arSA.numberingSystems
["arab"]
d8> arSA.timeZones
timeZones: ["Asia/Riyadh"]

d8> ja = new Intl.Locale("ja")
ja
d8> ja.calendars
["gregory", "japanese"]
d8> ja.collations
["unihan", "emoji", "eor"]
d8> ja.hourCycles
["h23"]
d8> ja.numberingSystems
["latn"]
d8> ja.timeZones
undefined

d8> jaJP = new Intl.Locale("ja-JP")
ja-JP
d8> jaJP.calendars
["gregory", "japanese"]
d8> jaJP.collations
["unihan", "emoji", "eor"]
d8> jaJP.hourCycles
["h23"]
d8> jaJP.numberingSystems
["latn"]
d8> jaJP.timeZones
["Asia/Tokyo"]}

d8> enUS = new Intl.Locale("en-US")
en-US
d8> enUS.calendars
["gregory"]
d8> enUS.collations
["emoji", "eor"]
d8> enUS.hourCycles
["h12"]
d8> enUS.numberingSystems
["latn"]
d8> enUS.timeZones
["America/Adak", "America/Anchorage", "America/Boise", "America/Chicago", "America/Denver", "America/Detroit", "America/Indiana/Knox", "America/Indiana/Marengo", "America/Indiana/Petersburg", "America/Indiana/Tell_City", "America/Indiana/Vevay", "America/Indiana/Vincennes", "America/Indiana/Winamac", "America/Indianapolis", "America/Juneau", "America/Kentucky/Monticello", "America/Los_Angeles", "America/Louisville", "America/Menominee", "America/Metlakatla", "America/New_York", "America/Nome", "America/North_Dakota/Beulah", "America/North_Dakota/Center", "America/North_Dakota/New_Salem", "America/Phoenix", "America/Sitka", "America/Yakutat", "Pacific/Honolulu"]

d8> enNZ = new Intl.Locale("en-NZ")
en-NZ
d8> enNZ.calendars
["gregory"]
d8> enNZ.collations
["emoji", "eor"]
d8> enNZ.hourCycles
["h12"]
d8> enNZ.numberingSystems
["latn"]
d8> enNZ.timeZones
["Pacific/Auckland", "Pacific/Chatham"]

d8> zh = new Intl.Locale("zh")
zh
d8> zh.calendars
["gregory", "chinese"]
d8> zh.collations
["pinyin", "big5han", "gb2312han", "stroke", "unihan", "zhuyin", "emoji", "eor"]
d8> zh.hourCycles
["h12"]
d8> zh.numberingSystems
["latn"]
d8> zh.timeZones
undefined

d8> zhTW = new Intl.Locale("zh-TW")      
zh-TW
d8>  zhTW.calendars
["gregory", "roc", "chinese"]
d8>  zhTW.collations
["stroke", "big5han", "gb2312han", "pinyin", "unihan", "zhuyin", "emoji", "eor"]
d8>  zhTW.hourCycles
["h12"]
d8>  zhTW.numberingSystems
["latn"]
d8>  zhTW.timeZones
["Asia/Taipei"]

d8> zhHK = new Intl.Locale("zh-HK")
zh-HK
d8> zhHK.calendars
["gregory", "chinese"]
d8> zhHK.collations
["stroke", "big5han", "gb2312han", "pinyin", "unihan", "zhuyin", "emoji", "eor"]
d8> zhHK.hourCycles
["h12"]
d8> zhHK.numberingSystems
["latn"]
d8> zhHK.timeZones
["Asia/Hong_Kong"]

d8> fa = new Intl.Locale("fa")
fa
d8> fa.calendars
["persian", "gregory", "islamic", "islamic-civil", "islamic-tbla"]
d8> fa.collations
["emoji", "eor"]
d8> fa.hourCycles
["h23"]
d8> fa.numberingSystems
["arabext"]
d8> fa.timeZones
undefined 

```

#### ~Unit Information~ DROPPED FEATURE

```js
l = new Intl.Locale("ar")
let unitInfo = l.unitInfo;
// {measurementSystem: "metric"}
l.unitInfo.measurementSystem
// metric
l = new Intl.Locale("en-GB")
l.unitInfo
// {measurementSystem: "uksystem"}
l = new Intl.Locale("en-GB")
l.unitInfo
// {measurementSystem: "uksystem"}
l = new Intl.Locale("en")
l.unitInfo
// {measurementSystem: "ussystem"}

```

