**#Homework-docker-sql**
To whom who is viewing it. This is my first time using Git Hub and I am really not sure if this is what the organizer asked for. Due to time limitation (It is the end of semester, so I am juggling with my academic while participating in this insightful zoomcamp), so I just copy and paste all the codes. Sorry for inconvinience. 

**## Question 1**
   ```bash
   docker run -it --entrypoint=bash python:3.12.8
   pip --version
```

**##Question 2**
```bash
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/green/green_tripdata_2019-10.csv.gz
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
docker-compose up -d
docker exec -it postgres bash
psql -U postgres -d ny_taxi
```

**## Question 3**
```{SQL}
SELECT 
    SUM(CASE WHEN trip_distance <= 1 THEN 1 ELSE 0 END) AS up_to_1_mile,
    SUM(CASE WHEN trip_distance > 1 AND trip_distance <= 3 THEN 1 ELSE 0 END) AS between_1_and_3_miles,
    SUM(CASE WHEN trip_distance > 3 AND trip_distance <= 7 THEN 1 ELSE 0 END) AS between_3_and_7_miles,
    SUM(CASE WHEN trip_distance > 7 AND trip_distance <= 10 THEN 1 ELSE 0 END) AS between_7_and_10_miles,
    SUM(CASE WHEN trip_distance > 10 THEN 1 ELSE 0 END) AS over_10_miles
FROM green_tripdata
WHERE 
    lpep_pickup_datetime >= '2019-10-01' AND 
    lpep_pickup_datetime < '2019-11-01';
```

**##Question 4**
```{SQL}
select 
Date(lpep_pickup_datetime) As trip_date,
Max(trip_distance) as max_trip_distance

from public.green_taxi_trips

GROUP BY trip_date
ORDER BY max_trip_distance desc;
```

**##Question 5**
```{SQL}
SELECT 
    b."Zone", 
    SUM(a.total_amount) AS total_amount 
FROM public.green_taxi_trips a
INNER JOIN public.taxi_zones b 
    ON a."PULocationID" = b."LocationID"
WHERE CAST(a.lpep_pickup_datetime AS DATE) = '2019-10-18'  
GROUP BY b."Zone" 
HAVING SUM(a.total_amount) > 13000  
ORDER BY total_amount DESC  
LIMIT 3;  
```

**##Question 6**
```{SQL}
SELECT 
    d."Zone",  
    c.LargestTip  
FROM (
    SELECT 
        a."DOLocationID",  -- Drop-off location ID
        MAX(a.tip_amount) AS LargestTip  
    FROM public.green_taxi_trips a
    INNER JOIN public.taxi_zones b 
        ON a."PULocationID" = b."LocationID"  
    WHERE CAST(a.lpep_pickup_datetime AS DATE) >= '2019-10-01' 
      AND CAST(a.lpep_pickup_datetime AS DATE) <= '2019-10-31'  
      AND b."Zone" = 'East Harlem North'  
    GROUP BY a."DOLocationID"  
) c 
INNER JOIN public.taxi_zones d 
    ON c."DOLocationID" = d."LocationID"  
ORDER BY c.LargestTip DESC 
LIMIT 1;  
```


