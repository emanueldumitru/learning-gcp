# Build Streaming data pipelines with Google Cloud 

Streaming real time information
Streaming is data processing for unbounded data sets
- infinite data set
- never complete

Online decisions

Pub/Sub - default retention of 7 days

control of number of subs / publishers / messages size and count


Pub/Sub Push versus Pull 
----------------------

pull model 7 days
push status 200 ok for HTTP call ACK 
acknowledgement, ackDeadline

pull/push subscription, ack 
set ackDeadline per Subscription


Message replay 
Subscribers can work as a team or separately

The limit is 10MB per message

### Highly recommended to implement a dead-letter sink and error logging!

Exponenential backoff, max delay, more delay added if an error
Security, monitoring and logging for Pub/Sub


Queueing issues that may rise

- latency
- out-of-order
- duplication 

You can use pub/sub with Dataflow to fix this sort of problems


Pub/Sub lab

```
export DEVSHELL_PROJECT_ID=$(gcloud config get-value project)
```


```
gcloud pubsub topics create sandiego

gcloud pubsub topics publish sandiego --message "hello"

gcloud pubsub subscriptions create --topic sandiego mySub1

gcloud pubsub subscriptions pull --auto-ack mySub1


gcloud pubsub topics publish sandiego --message "hello again"
gcloud pubsub subscriptions pull --auto-ack mySub1

gcloud pubsub subscriptions delete mySub1


gcloud pubsub subscriptions create --topic sandiego mySub2
gcloud pubsub subscriptions pull --auto-ack mySub2


gcloud pubsub subscriptions pull --auto-ack mySub2
```


# Streaming data with Dataflow, serverless service
apache beam


windowing
scalability ( handle the volume of data)
fault tolerance
model
timing, latency

Unbounded PCollection
Transform data with PTransform

Dataflow 
- fixed ( hourly, daily, monthly )
- sliding ( 5 minutes of data every 30 minutes )
- session ( communication is bursty, may correspond to a http session )

watermark - keep track of the lenght time of a window has been opened

afterwatermark - event time trigger
composite trigger


BiqQuery back in time 10 minutes query


```
SELECT *
FROM `demos.average_speeds`
FOR SYSTEM_TIME AS OF TIMESTAMP_SUB(CURRENT_TIMESTAMP, INTERVAL 10 MINUTE)
ORDER BY timestamp DESC
LIMIT 100
```

If you encounter this error please reduce the scope of your time travel by lowering the minute value.



# High throughput bigquery and bigtable

Streaming into BigQuery and use DataStudio

Streaming analytics and dashboards, create reports and charts to visualize datas



# Streaming into Cloud BigTable

lower latency big table, milliseconds or microseconds
higher throughput

Big table - colossus - tables and data - bigtable cluster vms

the rowkey is the index

scan sort search depends on the row key

BigTable Column Families

How to optmize data organization for performance:
- group related data for more efficient reads
- distribute data evenly for more efficient writes
- place identical values in the same row or adjoining rows for more efficient
compression

tablets

# Optimizing BigTable Performance

Hbase bigtable

- tune the schema
- cloud bigtable learning behavior
- tune the resources
- liniar performance improvement based on the number of the nodes added to the cluster
- clients and big table cluster are in the same zone



Hbase BigTable queries

```
scan 'current_conditions', {'LIMIT' => 2}

scan 'current_conditions', {'LIMIT' => 10, STARTROW => '15#S#1', ENDROW => '15#S#999', COLUMN => 'lane:speed'}
```


# Streaming into BigQuery

Analytic Window Functions
- standard aggregations
- navigation functions
- ranking and numbering functions



GIS Functions
- Geographic information system functions 
Performance Considerations


# Best practices for fast, smart data-driven decisions

- know your data - dataset
- ask good questions
- use queries effictively - sql 


1. avoid using unnecessary columns
2. some built-in functions are faster than others and all are faster that js udfs
3. filter early and often
4. order on the outermost query
5. join put the largest table on the left
6. use wildcards to query multiple tables
7. low cardinality is faster than high cardinality group by
8. use partitioned tables whenever you can

partition by DATE, TIMESTAMP or integer typed partition


Break queries into stages using intermediate tables, read only what is needed and store results at each step

!!! Processing is more expensive than storing data!!!


1. be purposeful in select

```
SELECT
  bike_id,
  duration
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire
ORDER BY
  duration DESC
LIMIT
  1
```

2. reduce data being read

```
SELECT
  MIN(start_station_name) AS start_station_name,
  MIN(end_station_name) AS end_station_name,
  APPROX_QUANTILES(duration, 10)[OFFSET (5)] AS typical_duration,
  COUNT(duration) AS num_trips
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire
WHERE
  start_station_id != end_station_id
GROUP BY
  start_station_id,
  end_station_id
ORDER BY
  num_trips DESC
LIMIT
  10
```

```
SELECT
  start_station_name,
  end_station_name,
  APPROX_QUANTILES(duration, 10)[OFFSET(5)] AS typical_duration,
  COUNT(duration) AS num_trips
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire
WHERE
  start_station_name != end_station_name
GROUP BY
  start_station_name,
  end_station_name
ORDER BY
  num_trips DESC
LIMIT
  10
```

3. reduce the number of expensive computations ( minimize the I/O)
4. Cache intermediate results 

```
CREATE OR REPLACE TABLE
  mydataset.typical_trip AS
SELECT
  start_station_name,
  end_station_name,
  APPROX_QUANTILES(duration, 10)[OFFSET (5)] AS typical_duration,
  COUNT(duration) AS num_trips
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire
GROUP BY
  start_station_name,
  end_station_name
```

```
WITH
typical_trip AS (
SELECT
  start_station_name,
  end_station_name,
  APPROX_QUANTILES(duration, 10)[OFFSET (5)] AS typical_duration,
  COUNT(duration) AS num_trips
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire
GROUP BY
  start_station_name,
  end_station_name )
SELECT
  EXTRACT (DATE
  FROM
    start_date) AS trip_date,
  APPROX_QUANTILES(duration / typical_duration, 10)[
OFFSET
  (5)] AS ratio,
  COUNT(*) AS num_trips_on_day
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire AS hire
JOIN
  typical_trip AS trip
ON
  hire.start_station_name = trip.start_station_name
  AND hire.end_station_name = trip.end_station_name
  AND num_trips > 10
GROUP BY
  trip_date
HAVING
  num_trips_on_day > 10
ORDER BY
  ratio DESC
LIMIT
10
```

5. Efficient joins

Avoid self-joins of large tables

```
CREATE OR REPLACE TABLE
  mydataset.london_bicycles_denorm AS
SELECT
  start_station_id,
  s.latitude AS start_latitude,
  s.longitude AS start_longitude,
  end_station_id,
  e.latitude AS end_latitude,
  e.longitude AS end_longitude
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire AS h
JOIN
  `bigquery-public-data`.london_bicycles.cycle_stations AS s
ON
  h.start_station_id = s.id
JOIN
  `bigquery-public-data`.london_bicycles.cycle_stations AS e
ON
  h.end_station_id = e.id
```

Materialized view

6. Use a window function instead of a self-join

```
SELECT
  bike_id,
  start_date,
  end_date,
  TIMESTAMP_DIFF( start_date, LAG(end_date) OVER (PARTITION BY bike_id ORDER BY start_date), SECOND) AS time_at_station
FROM
  `bigquery-public-data`.london_bicycles.cycle_hire
LIMIT
  5

```


```
WITH
unused AS (
  SELECT
    bike_id,
    start_station_name,
    start_date,
    end_date,
    TIMESTAMP_DIFF(start_date, LAG(end_date) OVER (PARTITION BY bike_id ORDER BY start_date), SECOND) AS time_at_station
  FROM
    `bigquery-public-data`.london_bicycles.cycle_hire )
SELECT
  start_station_name,
  AVG(time_at_station) AS unused_seconds
FROM
  unused
GROUP BY
  start_station_name
ORDER BY
  unused_seconds ASC
LIMIT
  5
```

7. Join with precomputed values

```
WITH
  distances AS (
  SELECT
    a.id AS start_station_id,
    a.name AS start_station_name,
    b.id AS end_station_id,
    b.name AS end_station_name,
    ST_DISTANCE(ST_GeogPoint(a.longitude,
        a.latitude),
      ST_GeogPoint(b.longitude,
        b.latitude)) AS distance
  FROM
    `bigquery-public-data`.london_bicycles.cycle_stations a
  CROSS JOIN
    `bigquery-public-data`.london_bicycles.cycle_stations b
  WHERE
    a.id != b.id ),
  durations AS (
  SELECT
    start_station_id,
    end_station_id,
    AVG(duration) AS duration,
    COUNT(*) AS num_rides
  FROM
    `bigquery-public-data`.london_bicycles.cycle_hire
  WHERE
    duration > 0
  GROUP BY
    start_station_id,
    end_station_id
  HAVING
    num_rides > 100 )
SELECT
  start_station_name,
  end_station_name,
  distance,
  duration,
  duration/distance AS pace
FROM
  distances
JOIN
  durations
USING
  (start_station_id,
    end_station_id)
ORDER BY
  pace ASC
LIMIT
  5
```

7. Limiting large sorts

```
SELECT
  rental_id,
  ROW_NUMBER() OVER(ORDER BY end_date) AS rental_number
FROM
  `bigquery-public-data.london_bicycles.cycle_hire`
ORDER BY
  rental_number ASC
LIMIT
  5
```
Cannot query rows larger than 100MB limit


Once your data is loaded inot bigquery, you are charged for storing it
- slots are units of processing resources
- flexible slots or flat-rate pricing

time out  6h 
default slots 2000