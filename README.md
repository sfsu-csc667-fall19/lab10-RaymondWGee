# Lab 9

## Docker Explaination
- king of like watered down VM because it doesnt need to fake the hardware (it just takes your bare minimum)
- runs exactly the same way on any machine (even if older version of node?)

- Dockerfile. Every docker image has to start off with what the parent image is
- somewhere in Docker repo, you can find pre-made images

- WORKDIR /main (creates a new working directory in /main)
- COPY . /main (copies everything in there into docker directory)
- RUN npm install is run inside docker. Since it is inside FROM container, its always
- node:10 installed

- EXPOSE 80 is just to open port to outside

- CMD is given an array of what to start (node index.js in this case)

## Basic Docker
- test basic index.js
- Install docker
- Build Docker image with  with `docker build -t hello-docker .`
- View your image with `docker image ls hello-docker`
- Run with `docker run -d -p 3000:3000 hello-docker`
- -d is detached (run in background)
- -p is port, mapping port 3000 to our port 3000. This bridges the ports.
- when it is running it counts as a VM
- if it works, it prints out a gigantic hash
- diff between image and container
- image is instructions how to create the application; a class
- container is like a object
- View with `docker container ls`
- `docker logs <id>` shows the logs of output
- Stop with `docker stop <container id>`
- Push your docker image with docker push https://docs.docker.com/engine/reference/commandline/push/

- tagged locally `docker tag hello-docker rgee5/hello-docker`
- then pushed with `docker push rgee5/hello-docker`

- tagged locally (generic)`docker tag <name> <dockeruser>/<name>`
- then pushed with `docker push <dockeruser>/<name>`

- Run your image off of dockerhub `docker run -d -p 3000:3000 <username>/hello-docker:v1`

- `docker pull <image>` on old versions, but newer just runs
- Try running someone else's image

## Inspecting docker containers
- Get into your contaienr with `docker exec -it <id> sh`
- <id> is the container id from docker container ls earlier
- ls now shows us the files we copied over
- this command opens a shell inside that docker machine
- You can now navigate and run commands from inside the container
- To get out, `exit`
- To view running logs `docker logs <id>`


- docker-compose file tells all the images you want to use
## Docker Swarm - container management system
- Enter swarm mode with `docker swarm init`
- makes your machine a swarm manager
- Try to join a swarm with `docker swarm join --token xxx`
- Deploy stack with `docker stack deploy -c docker-compose.yml swarm-of-hellos`
- View status with `docker service ls`
- Change replicas and redeploy
- Turn off stack with `docker stack remove swarm-of-hellos`
- Leave swarm with `docker swarm leave --force`

## Run on aws
- Install docker with `sudo snap install docker`
- Run with `sudo docker run -d -p 80:3000 <username>/hello-docker:v1`
- If you want to run the full stack, you will need the `docker-compose.yml` file

## TODO
- Install redis client
- To `index.js`, add a redis connection to the redis container
- Commit and push