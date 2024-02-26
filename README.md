### build an image

```docker
 docker image build -t web1 .
```

### run container

```docker
docker container run -it -p 5000 -e FLASK_APP=app.py --rm -d --name=web-1  web1:latest
```

```docker
 docker container run -it -p 5000 -e FLASK_APP=app.py -e FLASK_DEBUG=1 --rm -d --name=web1 -v $PWD:/app  web1:latest
```

### execute command

```docker
docker exec -it --user "$(id -u):$(id -g)"  web1 touch hi.txt
```

### testing new language

```docker
docker container run -it --rm --name testingnode node:hydrogen-alpine node
```

### create data volume

```
docker volume create web2_redis
```

```
docker container run -itd --rm -p 6379:6379 --net firstnetwork -v web2_redis:/data  --name redis redis:3.2-alpine
```

### create network

```
docker network create --driver bridge firstnetwork
```

### link container with network

```
 docker container run -itd --rm -p 6379:6379 --net firstnetwork  --name redis redis:3.2-alpine
```

### sharing data between containers

```
docker container run -it -p 5000:5000 -e FLASK_APP=app.py -e FLASK_DEBUG=1 --rm -d --net firstnetwork --name=web2 -v $PWD:/app -v /app/public  web2
```

```docker
docker container run -itd --rm -p 6379:6379 --net firstnetwork -v web2_redis:/data --volumes-from web2  --name redis redis:3.2-alpine
```

### stop all containers

```
docker container stop $(docker container ls -a -q)
```

### Remove all unused containers, networks, images

```
docker system prune
```
