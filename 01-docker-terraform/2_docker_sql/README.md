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