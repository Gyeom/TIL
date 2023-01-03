# PostgreSQL 날짜 및 시간 함수

### 자주 사용하는 함수
- date_part()
- extract()
- epoch
- to_char()
- to_date()

### 날짜 및 시간 관련 연산 기능 
| Operator | Example                                            | Result                          |
|----------|----------------------------------------------------|---------------------------------|
| +        | date '2001-09-28' + integer '7'                    | date '2001-10-05'               |
| +        | date '2001-09-28' + interval '1 hour'              | timestamp '2001-09-28 01:00:00' |
| +        | date '2001-09-28' + time '03:00'                   | timestamp '2001-09-28 03:00:00' |
| +        | interval '1 day' + interval '1 hour'               | interval '1 day 01:00:00'       |
| +        | timestamp '2001-09-28 01:00' + interval '23 hours' | timestamp '2001-09-29 00:00:00' |
| +        | time '01:00' + interval '3 hours'	                 | time '04:00:00'                 |
| +        | - interval '23 hours'                              | interval '-23:00:00'            |
| *        | 900 * interval '1 second'                          | 	interval '00:15:00'            |
| *        | 21 * interval '1 day'                              | interval '21 days'              |
| *        | double precision '3.5' * interval '1 hour'	        | interval '03:30:00'             |
| /        | interval '1 hour' / double precision '1.5'         | interval '00:40:00'             |

### 날짜 및 시간 관련 포멧팅
| Pattern                  | Description                                                                       |
|--------------------------|-----------------------------------------------------------------------------------|
| HH	                      | hour of day (01-12)                                                               |
| HH12                     | 	hour of day (01-12)                                                              |
| HH24	                    | hour of day (00-23)                                                               |
| MI                       | 	minute (00-59)                                                                   |
| SS	                      | second (00-59)                                                                    |
| MS	                      | millisecond (000-999)                                                             |
| US         	             | microsecond (000000-999999)                                                       |
| SSSS               	     | seconds past midnight (0-86399)                                                   |
| AM or A.M. or PM or P.M. | 	meridian indicator (uppercase)                                                   |
| am or a.m. or pm or p.m. | 	meridian indicator (lowercase)                                                   |
| Y,YYY	                   | year (4 and more digits) with comma                                               |
| YYYY                     | 	year (4 and more digits)                                                         |
| YYY                      | 	last 3 digits of year                                                            |
| YY                       | 	last 2 digits of year                                                            |
| Y                        | 	last digit of year                                                               |
| IYYY                     | 	ISO year (4 and more digits)                                                     |
| IYY                      | 	last 3 digits of ISO year                                                        |
| IY                       | 	last 2 digits of ISO year                                                        |
| I                        | 	last digits of ISO year                                                          |
| BC or B.C. or AD or A.D. | 	era indicator (uppercase)                                                        |
| bc or b.c. or ad or a.d. | 	era indicator (lowercase)                                                        |
| MONTH                    | 	full uppercase month name (blank-padded to 9 chars)                              |
| Month                    | 	full mixed-case month name (blank-padded to 9 chars)                             |
| month                    | 	full lowercase month name (blank-padded to 9 chars)                              |
| MON                      | 	abbreviated uppercase month name (3 chars in English, localized lengths vary)    |
| Mon                      | 	abbreviated mixed-case month name (3 chars in English, localized lengths vary)   |
| mon                      | 	abbreviated lowercase month name (3 chars in English, localized lengths vary)    |
| MM                       | 	month number (01-12)                                                             |
| DAY                      | 	full uppercase day name (blank-padded to 9 chars)                                |
| Day                      | 	full mixed-case day name (blank-padded to 9 chars)                               |
| day	                     | full lowercase day name (blank-padded to 9 chars)                                 |
| DY                       | 	abbreviated uppercase day name (3 chars in English, localized lengths vary)      |
| Dy                       | 	abbreviated mixed-case day name (3 chars in English, localized lengths vary)     |
| dy                       | 	abbreviated lowercase day name (3 chars in English, localized lengths vary)      |
| DDD                      | 	day of year (001-366)                                                            |
| DD                       | 	day of month (01-31)                                                             |
| D                        | 	day of week (1-7; Sunday is 1)                                                   |
| W                        | 	week of month (1-5) (The first week starts on the first day of the month.)       |
| WW                       | 	week number of year (1-53) (The first week starts on the first day of the year.) |
| IW                       | 	ISO week number of year (The first Thursday of the new year is in week 1.)       |
| CC                       | 	century (2 digits) (The twenty-first century starts on 2001-01-01.)              |
| J                        | 	Julian Day (days since January 1, 4712 BC)                                       |
| Q                        | 	quarter                                                                          |
| RM                       | 	month in Roman numerals (I-XII; I=January) (uppercase)                           |
| rm                       | 	month in Roman numerals (i-xii; i=January) (lowercase)                           |
| TZ                       | 	time-zone name (uppercase)                                                       |
| tz                       | 	time-zone name (lowercase)                                                       |
||
