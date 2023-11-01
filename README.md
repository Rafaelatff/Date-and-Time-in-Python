# Date-and-Time-in-Python
Repositorie to gather my knowledge during my course on DataCamp.

## Date

Represented on US stile : mm/dd/YYYY. To create a date class, we need:
(ISO 8601 format) = .isoformat() % YYYY/mm/dd

```py
from datetime import date

# Creating dates
two_dates = [date(2010, 8, 22), date(2017, 6, 21)] # Cannot have 08 as month, need to be 8
```

It is possible to access the individual atributes from the dates:

```py
print(two_dates[0].year)
print(two_dates[0].weekday()) # To return the number of weekday
```

For the weekday() method we have:

* 0 = Monday
* 1 = Tuesday
* 2 = Wednesday
* 3 = Thursday
* 4 = Friday
* 5 = Saturday
* 6 = Sunday

##  Math with dates

It is possible to insert the dates in a list and then get its `.min()` date, or even the diference of days between then `print(delta.days)`.
We can also create timedeltas, by:

```py
from datetime import timedelta

# Creating a timedelta
td = timedelta(days=20)
print (date + td)
```

## Turning dates into strings and formating

To express the date in ISO 8601 format and put it in a list:

```py
print([date.isoformat()])
```

```py
print(date.strftime("%Y")) # Return a string with only the year, and its 4 digits
print(date.strftime("%y")) # only 2 digits of yeAR
print(date.strftime("Year is %Y"))
print(date.strftime("%Y/%m/%d"))
print(date.strftime("%B") # Print the month like 'August'
print(date.strftime("%j") # Print the day of the year, from 0 to 365
```

## Date and time

To use date and time together:

```py
from datetime import datetime

dt = datetime(2017, 10, 1, 15, 23, 25) # Y, m, d, h, m, s 
dt = datetime(2017, 10, 1, 15, 23, 500000) # second as microseconds
dt = datetime(year=2017, month=10, day=1, 
	 	hour=15, minute=23, second=25,
		microsecond=500000) # also works
```
To replace a value:

```py
new_hr = dt.replace(minute=0, second=0, microsecond=0)
```

## Printing date and time

```py
print(dt.strftime("%Y-%m-%d %H:%M:%S"))
print(dt.isoformat()) #YYYY-mm-ddTHH:MM:SS
```

To get datetime from string, we use `strptime`, string parse time.

```py
from datetime import datetime

dt = datetime.strptime("12/30/2017 15:19:13", 
			"%m/%d/%Y %H:%M:%S%") # following the string position
```

## Time stamp

Is the number of seconds since January 1st, 1970. This date is considered the birth of modern computers.
To read an unix datetime, just:

```py
ts = 1514665153.0

print(datetime.fromtimestamp(ts)) # It returns a datetime
```

## Durations

How to use:

```py
duration = start - end
print(duration.total_seconds())
```

Doing from hand:
```py
from datetime import timedelta

delta1 = timedelta(seconds=1)
delta2 = timedelta(days=1, seconds=1)
delta3 = timedelta(weeks=-1)
start + delta3
```

## UTC offsets

```py 
from datetime import datetime, timedelta, timezone

# US Eastern Standad time zone
ET = timezone(timedelta(hours=-5))
# India Standad time zone
IST = timezone(timedelta(hours=5, minutes=30))
# AEDT = Australian Eastern Daylight Time
aedt = timezone(timedelta(hours=11))

dt = datetime(2017, 12, 30, 15, 9, 10, tzinfo = ET)
# Printing it will return: 2017-12-30 15:09:10-05:00

print(dt.astimezone(IST)) # Set the clock -10:30 before US Eastern
# It will return: 2017-12-31 01:39:10+05:30

print(dt.replace(tzinfo=timezone.utc)) # +00:00, and returns 15h
print(dt.astimezone(timezone.utc)) # +00:00, and returns 20h

## Timezone database

There is a global database will all the timezones that are updated accoding with the seasons.

```py
from datetime import datetime
from dateutil import tz # Database

# Eastern time
et =tz.gettz('America/New_Yourk') # Format: 'Continent/City'

```

Note: Attention to start and ending of daylight saving time. In some cases. it may have two 1 A.M. To check if thhis could happen, we give a time to a variable first_1am and then we use `tz.datetime_ambiguous(first_1am)`.



