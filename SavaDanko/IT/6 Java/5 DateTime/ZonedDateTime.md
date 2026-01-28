#java 

---
`ZonedDateTime` is an immutable representation of a date-time with a time-zone.


###### **now**
```java
public static ZonedDateTime now()
```
Obtains the current date-time from the system clock in the default time-zone.

###### **of**
```java
public static ZonedDateTime of(LocalDate date,
													LocalTime time,
												    ZoneId zone)
```
Obtains an instance of `ZonedDateTime` from a local date and time.

###### **of**
```java
public static ZonedDateTime of(int year,
													int month,
													int dayOfMonth,
													int hour,
													int minute,
													int second,
													int nanoOfSecond,
													ZoneId zone)
```
Obtains an instance of `ZonedDateTime` from a year, month, day, hour, minute, second, nanosecond and time-zone.

###### **parse**
```java
public static ZonedDateTime parse(CharSequence text,
														 DateTimeFormatter formatter)
```

###### **getZone**
```java
public ZoneId getZone()
```
Gets the time-zone, such as 'Europe/Paris'.

###### **getMonth**
```java
public Month getMonth()
```
Gets the month-of-year field using the `Month` enum.

###### **getMinute**
```java
public int getMinute()
```
Gets the minute-of-hour field.

###### **plus**
```java
public ZonedDateTime plus(long amountToAdd,
											  TemporalUnit unit)
```
Returns a copy of this date-time with the specified amount added.

###### **minus**
```java
public ZonedDateTime minus(long amountToSubtract,
												 TemporalUnit unit)
```
Returns a copy of this date-time with the specified amount subtracted.

###### **format**
```java
public String format(DateTimeFormatter formatter)
```
Formats this date-time using the specified formatter.

