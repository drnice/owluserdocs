---
description: UTC + global DateTime standard
---

# Owl Time Zone API

### Background on common time issues

Controlling dates and times has always been a troublesome topic for global systems.  Server clock vs server code such as new Date\(\)  which may create a date in the local timezone of the server vs the Browser or clients timezone.  Moving to the cloud only makes the problem worse when you need to consider the timezone the server might be in and inherit from it's system clock.

### Owl's Solution - Keep it Simple

If everyone worked off of a globally understood format that is not subject to misinterpretation things would be more simple.  Example:  03/02/2019  is this March second or Feb 3rd?  Depends which country you live in.  Owl only accepts this format:  2019-03-02.  Extending this to time would mean 2019-03-02 00:00:00

### CmdLine Examples

./owlcheck -ds trades -rd  "2019-04-01"    or   -rd  "2019-04-01 00:00:00"

### Simple Example

A user running an OwlCheck in New York and a user running an OwlCheck 3 hrs later in CA.

| CmdLine Arg | User Location | TimeZone | Stored in Owl \(UTC\) |
| :--- | :--- | :--- | :--- |
| -rd 2019-04-01 | New York | implied EST | 2019-04-01 04:00:00 |
| -rd 2019-04-01 | California | implied PST | 2019-04-01 07:00:00 |

As you can see these jobs actually run 3 hrs apart even though they appear to run first thing in the morning to each user.  Owl stores all dates in a common **UTC** format for global consistency.

### Web API or URL Example

[http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01](http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01) 04:00:00 [http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01](http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01) 07:00:00

#### For Convenience if a user prefers seeing and interacting with dates in their local time zone

[http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01](http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01) 00:00:00&tz=EST [http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01](http://localhost:9000/dq/hoot?dataset=atmCustomers&runId=2019-04-01) 00:00:00&tz=PST

