
https://docs.docker.com/engine/reference/commandline/run/

Assign name and allocate pseudo-TTY (--name, -it)🔗
docker run --name py-etl-training -it brentgroves/py-etl-training

Run docker exec on a running container🔗
First, start a container.

 docker run --name ubuntu_bash --rm -i -t ubuntu bash

docker run --name send-email-docker --rm -i -t brentgroves/send-email-docker:1 /bin/bash


docker run --name send-email-docker --rm -i -t brentgroves/send-email-docker:1 /bin/bash