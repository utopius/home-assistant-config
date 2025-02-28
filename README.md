# My Home Assistant Configuration

This is my personal Home Assistant configuration, running my home automations.

## Useful queries

### States

```sql
SELECT m.entity_id, m.metadata_id, s.state_id, datetime(ROUND(s.last_reported_ts), 'unixepoch') as last_reported, datetime(ROUND(s.last_updated_ts), 'unixepoch') as last_updated, state
FROM states s
LEFT JOIN states_meta m
ON s.metadata_id = m.metadata_id
WHERE m.entity_id = "sensor.heat_meter_total_last_year"
```

```sql
UPDATE states
SET state = 96495.0
WHERE metadata_id = 6420 AND state > 96495.0
```

### Short-term statistics

Some borked statistics values left in the graphs? Then there are leftovers in the short-term statistics table.

```sql
SELECT m.statistic_id as entity_id, m.id as meta_id, s.id, datetime(ROUND(s.created_ts), 'unixepoch') as created_date, datetime(ROUND(s.start_ts), 'unixepoch') as start_date, s.min, s.mean, s.max, s.state, s.sum
FROM statistics_short_term s
LEFT JOIN statistics_meta m
ON s.metadata_id = m.id
WHERE m.statistic_id = "sensor.heat_meter_total_last_year" AND state > 96495.0
ORDER BY created_ts ASC
```

```sql
UPDATE statistics_short_term
SET state = 96495.0
WHERE metadata_id = 428 AND state = 0.0
```

### Long-term statistics

```sql
SELECT m.statistic_id as entity_id, m.id as meta_id, s.id, datetime(ROUND(s.created_ts), 'unixepoch') as created_date, datetime(ROUND(s.start_ts), 'unixepoch') as start_date, s.min, s.mean, s.max, s.state, s.sum
FROM statistics s
LEFT JOIN statistics_meta m
ON s.metadata_id = m.id
WHERE m.statistic_id = "sensor.heat_meter_total_last_year" AND state > 96495.0
ORDER BY created_ts ASC
```

```sql
UPDATE statistics
SET state = 96495.0
WHERE metadata_id = 428 AND state = 0
```

## License

MIT License

Copyright (c) 2024-2025 Florian Herbel

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