# Backend Load Tests

Run with `artillery run (courses.yml|landing.yml|rate-limit.yml)`. 

Tests cover potential high load scenarios:
- `courses.yml` - a marketing campaign skyrockets and many users want to see the launched courses
- `landing.yml` - a marketing campaign skyrockets and many users open the user area, fetching some initial data of their account
- `rate-limit.yml` - a (malicious) third party runs into rate limiting while trying to scrape emails


## 28-05-2022

With 300 requests/s we can serve 18.000 requests per minute which is half of our userbase. So that seems to be performant enough.
The rate limiter could be faster (i.e. by exiting before actually parsing the query), but we won't win against a DDOS anyway.

Public Courses:

```
errors.ETIMEDOUT: .............................................................. 1
http.codes.200: ................................................................ 23999
http.request_rate: ............................................................. 364/sec
http.requests: ................................................................. 24000
http.response_time:
  min: ......................................................................... 2
  max: ......................................................................... 1079
  median: ...................................................................... 41.7
  p95: ......................................................................... 804.5
  p99: ......................................................................... 1002.4
```

Landing Page (Fetching Matches and Courses for one user):

```
errors.ETIMEDOUT: .............................................................. 1
http.codes.200: ................................................................ 20999
http.request_rate: ............................................................. 308/sec
http.requests: ................................................................. 21000
http.response_time:
  min: ......................................................................... 15
  max: ......................................................................... 1043
  median: ...................................................................... 40.9
  p95: ......................................................................... 55.2
  p99: ......................................................................... 71.5
```

Rate Limit:

```
http.codes.200: ................................................................ 21000
http.request_rate: ............................................................. 308/sec
http.requests: ................................................................. 21000
http.response_time:
  min: ......................................................................... 15
  max: ......................................................................... 1047
  median: ...................................................................... 40
  p95: ......................................................................... 51.9
  p99: ......................................................................... 71.5
```


