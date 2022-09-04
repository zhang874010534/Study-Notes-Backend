```sql
// 今日
SELECT id,max(toDate(time)) from resourcesPerformance  where toDate(time) = today() group by id
// 本周
SELECT id,max(toDate(time)) from resourcesPerformance  where toUnixTimestamp(time) between toUnixTimestamp(now()) - 60 * 60 * 24 * toDayOfWeek(now()) and  toUnixTimestamp(now()) + 60 * 60 * 24 * ( 7- toDayOfWeek(now()))  group by id
// 本月
SELECT id,max(toDate(time)) from resourcesPerformance  where toMonth(time) = toMonth(now())  group by id
```

