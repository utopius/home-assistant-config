# My Home Assistant Configuration

This is my personal Home Assistant configuration, running my home automations.

## Useful queries

### States

```sql
SELECT m.entity_id, m.metadata_id, s.state_id, datetime(ROUND(s.last_reported_ts), 'unixepoch') as last_reported, datetime(ROUND(s.last_updated_ts), 'unixepoch') as last_updated, state
FROM states s
LEFT JOIN states_meta m
ON s.metadata_id = m.metadata_id
WHERE m.entity_id = "sensor.heat_meter_daily_usage"
```

### Short-term statistics

```sql
SELECT m.statistic_id as entity_id, m.id as meta_id, s.id, datetime(ROUND(s.created_ts), 'unixepoch') as created_date, datetime(ROUND(s.start_ts), 'unixepoch') as start_date, s.min, s.mean, s.max, s.state, s.sum
FROM statistics_short_term s
LEFT JOIN statistics_meta m
ON s.metadata_id = m.id
WHERE m.statistic_id = "sensor.heat_meter_daily_usage"
AND strftime('%s', created_date ) BETWEEN strftime('%s', "2024-11-01 00:00:00") AND strftime('%s', "2024-11-02 00:00:00")
ORDER BY created_ts ASC
```

### Long-term statistics

```sql
SELECT m.statistic_id as entity_id, m.id as meta_id, s.id, datetime(ROUND(s.created_ts), 'unixepoch') as created_date, datetime(ROUND(s.start_ts), 'unixepoch') as start_date, s.min, s.mean, s.max, s.state, s.sum
FROM statistics s
LEFT JOIN statistics_meta m
ON s.metadata_id = m.id
WHERE m.statistic_id = "sensor.heat_meter_daily_usage"
ORDER BY created_ts ASC
```

## License

MIT License

Copyright (c) 2018-2022 Franck Nijhof

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.