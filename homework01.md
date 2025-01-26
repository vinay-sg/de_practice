## Sol 1. Understanding docker first run 

```
docker pull python:3.12.8 //pull the respective image
docker run -it python:3.12.8 bash // run the container using the image in an iterative+attached terminal mode with bash command
pip --version // output is 24.3.1
```

## Sol 2. Understanding Docker networking and docker-compose

```
the db is accessible at db:5432
```

## Sol 3. Trip Segmentation Count

```sql
select count(*) as upto_1_mile
from green_taxi_201910
where lpep_pickup_datetime >= '2019-10-01 00:00:00' and lpep_dropoff_datetime < '2019-11-01 00:00:00'
and trip_distance<=1

select count(*) as between_1_3
from green_taxi_201910
where lpep_pickup_datetime >= '2019-10-01 00:00:00' and lpep_dropoff_datetime < '2019-11-01 00:00:00'
and trip_distance>1 and trip_distance<=3

select count(*) as between_3_7
from green_taxi_201910
where lpep_pickup_datetime >= '2019-10-01 00:00:00' and lpep_dropoff_datetime < '2019-11-01 00:00:00'
and trip_distance>3 and trip_distance<=7

select count(*) as between_7_10
from green_taxi_201910
where lpep_pickup_datetime >= '2019-10-01 00:00:00' and lpep_dropoff_datetime < '2019-11-01 00:00:00'
and trip_distance>7 and trip_distance<=10

select count(*) as over_10
from green_taxi_201910
where lpep_pickup_datetime >= '2019-10-01 00:00:00' and lpep_dropoff_datetime < '2019-11-01 00:00:00'
and trip_distance>10
```

## Sol 4. Longest trip for each day

```sql
select lpep_pickup_datetime
from green_taxi_201910
order by trip_distance desc
limit 1
```

## Sol 5. Three biggest pickup zones
```sql
select zones."Zone" as "zone",
sum(total_amount) as total
from green_taxi_201910 inner join zones on 
green_taxi_201910."PULocationID" = zones."LocationID"
where date(lpep_pickup_datetime)='2019-10-18'
group by zones."Zone"
having sum(total_amount)>13000
order by total desc
```

## Sol 6. Largest tip
```sql
select 
    z."Zone" as drop_off_zone, 
    max(t.tip_amount) as max_tip
from green_taxi_201910 as t
join zones as pz on t."PULocationID" = pz."LocationID"
join zones as z on t."DOLocationID" = z."LocationID"
where pz."Zone" = 'East Harlem North'
  and t.lpep_pickup_datetime >= '2019-10-01 00:00:00'
  and t.lpep_pickup_datetime < '2019-11-01 00:00:00'
group by z."Zone"
order by max_tip desc
limit 1;
```

## Sol 7. Terraform Workflow
```sh
terraform init
terraform apply -auto-approve
terraform destroy
```
