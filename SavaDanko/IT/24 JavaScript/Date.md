#js 

---
[`jsref_obj_date`](https://www.w3schools.com/jsref/jsref_obj_date.asp)

---
JavaScript `Date Objects` let us work with dates:
```js
const d = new Date();
```
Date objects are static. The "clock" is not "running".

By default, JavaScript will use the browser's time zone and display a date as a full text string:
`Mon Jul 21 2025 11:13:56 GMT+0300 (Moscow Standard Time)`

###### **Creating Date Objects**
Date objects are created with the `new Date()` constructor.
There are 9 ways to create a new date object:
```js
new Date()
new Date(date string)

new Date(year,month)
new Date(year,month,day)
new Date(year,month,day,hours)
new Date(year,month,day,hours,minutes)
new Date(year,month,day,hours,minutes,seconds)
new Date(year,month,day,hours,minutes,seconds,ms)

new Date(milliseconds)
```

###### **new Date()**
`new Date()` creates a date object with the current date and time:
```js
const d = new Date();
```

###### **new Date(date string)**
`new Date(date string)` creates a date object from a date string:
```js
 const d = new Date("October 13, 2014 11:13:00");
 const d = new Date("2022-03-25");
```

###### **new Date(year, month, ...)**
`new Date(_year, month, ..._)` creates a date object with a specified date and time.
7 numbers specify year, month, day, hour, minute, second, and millisecond (in that order):
```js
const d = new Date(2018, 11, 24, 10, 33, 30, 0);
```
JavaScript counts months from 0 to 11:
- January = 0.
- December = 11.

###### **Displaying Dates**
JavaScript will (by default) output dates using the `toString()` method. This is a string representation of the date, including the time zone. The format is specified in the ECMAScript specification:
`Mon Jul 21 2025 11:13:56 GMT+0300 (Moscow Standard Time)`

When you display a date object in HTML, it is automatically converted to a string, with the `toString()` method.

The `toDateString()` method converts a date to a more readable format:
```js
const d = new Date();  
d.toDateString();
```

The `toUTCString()` method converts a date to a string using the UTC standard:
```js
const d = new Date();  
d.toUTCString();
```

###### **JavaScript Date Formats**
JavaScript ISO Dates:
ISO 8601 is the international standard for the representation of dates and times.
The ISO 8601 syntax `(YYYY-MM-DD`) is also the preferred JavaScript date format:
```js
const d = new Date("2015-03-25");
```

ISO Dates (Date-Time):
ISO dates can be written with added hours, minutes, and seconds (`YYYY-MM-DDTHH:MM:SSZ`):
```js
const d = new Date("2015-03-25T12:00:00Z");
```

###### **Date Input - Parsing Dates**
If you have a valid date string, you can use the `Date.parse()` method to convert it to milliseconds.
`Date.parse()` returns the number of milliseconds between the date and January 1, 1970:
```js
let msec = Date.parse("March 21, 2012");
```

###### **`getFullYear()`**
The `getFullYear()` method returns the year of a date as a four digit number:
```js
const d = new Date("2021-03-25");  
d.getFullYear();
```

###### **`getMonth()`**
The `getMonth()` method returns the month of a date as a number (0-11).
```js
const d = new Date("2021-03-25");  
d.getMonth();
```

###### **`getDate()`**
The `getDate()` method returns the day of a date as a number (1-31):
```js
const d = new Date("2021-03-25");  
d.getDate();
```

###### **`getHours()`**
The `getHours()` method returns the hours of a date as a number (0-23):
```js
const d = new Date("2021-03-25");  
d.getHours();
```

###### **`getMinutes()`**
The `getMinutes()` method returns the minutes of a date as a number (0-59):
```js
const d = new Date("2021-03-25");  
d.getMinutes();
```

###### **`getSeconds()`**
The `getSeconds()` method returns the seconds of a date as a number (0-59):
```js
const d = new Date("2021-03-25");  
d.getSeconds();
```

###### **`getMilliseconds()`**
The `getMilliseconds()` method returns the milliseconds of a date as a number (0-999):
```js
const d = new Date("2021-03-25");  
d.getMilliseconds();
```

###### **`getDay()`**
The `getDay()` method returns the weekday of a date as a number (0-6).
```js
const d = new Date("2021-03-25");  
d.getDay();
```

###### **`getTime()`**
The `getTime()` method returns the number of milliseconds since January 1, 1970:
```js
const d = new Date("1970-01-01");  
d.getTime();
```

###### **`Date.now()`**
`Date.now()` returns the number of milliseconds since January 1, 1970.
```js
let ms = Date.now();
```

###### **`getTimezoneOffset()`**
The `getTimezoneOffset()` method returns the difference (in minutes) between local time an UTC time:
```js
let diff = d.getTimezoneOffset();
```

###### **`setFullYear()`**
The `setFullYear()` method sets the year of a date object. In this example to 2020:
```js
const d = new Date("January 01, 2025");  
d.setFullYear(2020);
```

###### **`setMonth()`**
The `setMonth()` method sets the month of a date object (0-11):
```ls
const d = new Date("January 01, 2025");  
d.setMonth(11);
```

###### **`setDate()`**
The `setDate()` method sets the day of a date object (1-31):
```js
const d = new Date("January 01, 2025");  
d.setDate(15);
```

###### **`setHours()`**
The `setHours()` method sets the hours of a date object (0-23):
```js
const d = new Date("January 01, 2025");  
d.setHours(22);
```

###### **`setMinutes()`**
The `setMinutes()` method sets the minutes of a date object (0-59):
```js
const d = new Date("January 01, 2025");  
d.setMinutes(30);
```

###### **`setSeconds()`**
The `setSeconds()` method sets the seconds of a date object (0-59):
```js
const d = new Date("January 01, 2025");  
d.setSeconds(30);
```

###### **Compare Dates**
Dates can easily be compared.
The following example compares today's date with January 14, 2100:
```js
let text = "";  
const today = new Date();  
const someday = new Date();  
someday.setFullYear(2100, 0, 14);  
  
if (someday > today) {  
  text = "Today is before January 14, 2100.";  
} else {  
  text = "Today is after January 14, 2100.";  
}
```
