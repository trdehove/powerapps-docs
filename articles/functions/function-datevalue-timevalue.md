<properties
	pageTitle="PowerApps: DateValue, TimeValue, and DateTimeValue functions"
	description="Reference information for the DateValue, TimeValue, and DateTimeValue functions in PowerApps, including syntax and examples"
	services=""
	suite="powerapps"
	documentationCenter="na"
	authors="gregli-msft"
	manager="dwrede"
	editor=""
	tags=""/>

<tags
   ms.service="powerapps"
   ms.devlang="na"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="11/07/2015"
   ms.author="gregli"/>

# DateValue, TimeValue, and DateTimeValue functions in PowerApps #

Converts date and times in a string to a date/time value.

## Description ##

The **DateValue** function converts a date string to a date/time value.  For example, "10/01/2014".

The **TimeValue** function converts a time string to a date/time value.  For example, "12:15 PM".

The **DateTimeValue** functions converts to a date and time string to a date/time value.  For example, "January 10, 2013 12:13 AM".

If time information is included in the argument to **DateValue** or date information is include in the argument to **TimeValue**, it is ignored.

By default the language used is that of the current user, but you can override this to ensure that strings are interpreted properly.  For example "10/1/1920" is interpreted as October 1<sup>st</sup> in "en" and as January 10<sup>th</sup> in "fr".

Dates must be in one of the following formats:

- MM/DD/YYYY
- DD/MM/YYYY
- DD Mon YYYY
- Month DD, YYYY

See the **[Date](function-date-time.md)** and **[Time](function-date-time.md)** functions to convert from numbers.

Also see [working with dates and times](../show-text-dates-times.md) for more information.

## Syntax ##

**DateValue**( *String* [, *Language* )
**DateTimeValue**( *String* [, *Language* )
**TimeValue**( *String* [, *Language* )

- *String* - Required.  A text string containing a date, time, or combination date and time value.
- *Language* - Optional.  A language string, such as would be returned by the first two characters from the **[Language](function-language.md)** function.  If not provided, the language of the current user's client is used.  

## Examples ##

### DateValue ###

If you typed **10/11/2014** into an input-text control named **Startdate** and then set the **Text** property of a label to this function:

- **Text(DateValue(Startdate!Text), DateTimeFormat!LongDate)**

	The label would show **Saturday, October 11, 2014**, if your computer were set to the **en** locale.

	**Note:** You can use several options, other than **LongDateTime**, with the **DateTimeFormat** parameter. To display a list of those options, type the parameter, followed immediately by an exclamation point, in the function box.

- **Text(DateValue(Startdate!Text, "fr"), DateTimeFormat!LongDate)**

	The label would show **Monday, November 10, 2014**.

If you did the same thing on October 20, 2014:

- **DateDiff(DateValue(Startdate!Text), Today())**

	If your computer were set to the **en** language, the label would show **9**, indicating the number of days between October 11 and October 20. **DateDiff** can also show the difference in months, quarters, or years.

### DateTimeValue ###

If you typed **10/11/2014 1:50:24.765 PM** into an input-text control named **Start** and then set the **Text** property of a label to this function:

- **Text(DateTimeValue(Start!Text), DateTimeFormat!LongDateTime)**

	The label would show **Saturday, October 11, 2014 1:50:24 PM** if your computer were set to the "en" locale.

	**Note:** You can use several options, other than LongDateTime, with the DateTimeFormat parameter. To display a list of those options, type the parameter, followed immediately by an exclamation point, in the function box.

- **Text(DateTimeValue(Start!Text, "fr"), DateTimeFormat!LongDateTime)**

	The label would show **Monday, November 10, 2014 1:50:24 PM**.

- **Text(DateTimeValue(Start!Text), "dddd, mmmm dd, yyyy hh:mm:ss.fff AM/PM")**

	The label would show **Saturday, October 11, 2014 01:50:24:765 PM** if your computer were set to the **en** locale.

	As an alternative, you can specify hh:mm:ss.f or hh:mm:ss.ff to round the time to the nearest tenth or hundredth of a second.

### TimeValue ###

Name an input-text control FinishedAt, and set the Text property of a label to this function:

If(TimeValue(FinishedAt!Text)<TimeValue("5:00:00.000 PM"), "You made it!", "Too late!")

- If you type 4:59:59.999 PM into the FinishedAt control, the label shows "You made it!"

- If you type 5:00:00.000 PM into the FinishedAt control, the label shows "Too late!"