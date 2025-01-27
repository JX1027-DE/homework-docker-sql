**#Homework-docker-sql**
To whom who is viewing it. This is my first time using Git Hub and I am really not sure if this is what the organizer asked for. Due to time limitation (It is the end of semester, so I am juggling with my academic while participating in this insightful zoomcamp), so I just copy and paste all the codes. Sorry for inconvinience. 

**## Question 1**
   ```bash
   docker run -it --entrypoint=bash python:3.12.8
   pip --version

**##Question 2**
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/green/green_tripdata_2019-10.csv.gz
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
docker-compose up -d
docker exec -it postgres bash
psql -U postgres -d ny_taxi

**## Question 3**
SELECT
    SUM(CASE WHEN trip_distance <= 1 THEN 1 ELSE 0 END) AS up_to_1_mile,
    SUM(CASE WHEN trip_distance > 1 AND trip_distance <= 3 THEN 1 ELSE 0 END) AS between_1_and_3_miles,
    SUM(CASE WHEN trip_distance > 3 AND trip_distance <= 7 THEN 1 ELSE 0 END) AS between_3_and_7_miles,
    SUM(CASE WHEN trip_distance > 7 AND trip_distance <= 10 THEN 1 ELSE 0 END) AS between_7_and_10_miles,
    SUM(CASE WHEN trip_distance > 10 THEN 1 ELSE 0 END) AS over_10_miles
FROM green_taxi_trips
WHERE lpep_pickup_datetime >= '2019-10-01'
  AND lpep_pickup_datetime < '2019-11-01'
  AND lpep_dropoff_datetime < '2019-11-01';
