docker run hello-world

### Interactive mode (-it)
docker run -it ubuntu bash
docker run -it python:3.9

docker run -it --entrypoint=bash python:3.9
pip install pandas

Ctrl + D : exit python mode
exit : exit docker

pandas.__version__

### Run from Dockerfile
docker build -t test:pandas .
docker run -it test:pandas

### Run Postgres with Docker

docker run -it \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v /workspaces/ZoomCamp2024/01-docker-terraform/2_docker_sql/ny_taxi_postgres_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:13

pgcli -h localhost -p 5432 -u root -d ny_taxi

docker run -it \
  -e PGADMIN_DEFAULT_EMAIL="admin@admin.com" \
  -e PGADMIN_DEFAULT_PASSWORD="root" \
  -p 8080:80 \
  dpage/pgadmin4

docker network create pg-network

docker run -it \
  -e POSTGRES_USER="root" \
  -e POSTGRES_PASSWORD="root" \
  -e POSTGRES_DB="ny_taxi" \
  -v /workspaces/ZoomCamp2024/01-docker-terraform/2_docker_sql/ny_taxi_postgres_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  --network=pg-network \
  --name pg-database \
  postgres:13

docker run -it \
  -e PGADMIN_DEFAULT_EMAIL="admin@admin.com" \
  -e PGADMIN_DEFAULT_PASSWORD="root" \
  -p 8080:80 \
  --network=pg-network \
  --name pgadmin-2 \
  dpage/pgadmin4

select *
from yellow_taxi_data
where index > 100000
where (tpep_pickup_datetime >= '2019-09-18 00:00:00') and (tpep_dropoff_datetime <= '2019-09-19 00:00:00')

year("tpep_pickup_datetime") = 2019

# Question 3
select count(*) from green_taxi_data
where (lpep_pickup_datetime >= '2019-09-18 00:00:00') and (lpep_dropoff_datetime < '2019-09-19 00:00:00')

-> 15612

# Question 4
select lpep_pickup_datetime, (lpep_dropoff_datetime - lpep_pickup_datetime ) as "trip_time" from green_taxi_data
order by trip_time desc

-> 2019-09-26

# Question 5
select "PULocationID", count(*) as cnt from green_taxi_data
where (lpep_pickup_datetime >= '2019-09-18 00:00:00') and (lpep_pickup_datetime < '2019-09-19 00:00:00')
group by "PULocationID"
order by cnt desc