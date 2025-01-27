# homework-docker-sql
# To whom who is viewing it. This is my first time using Git Hub and I am really not sure if this is what the organizer asked for. Due to time limitation (It is the end of semester, so I am juggling with my academic while participating in this insightful zoomcamp), so I just copy and paste all the codes. Sorry for inconvinience. 

## Question 1: Understanding Docker First Run
docker run -it python:3.12.8 bash
pip --version

**## Question 2: Understanding Docker First Run**
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/green/green_tripdata_2019-10.csv.gz
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
docker-compose up -d
docker exec -it postgres bash
psql -U postgres -d ny_taxi

**## Question 3: Trip Segmentation Count**

