# start a container in the background
docker run --name etl-pod -d brentgroves/etl-pod:2
docker container ls -a

# Next, execute a command on the container.
docker exec -it etl-pod pwd
docker exec -it etl-pod pgrep cron

# Next, execute an interactive bash shell on the container.
docker exec -it etl-pod bash
