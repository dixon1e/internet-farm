## Hack the DOT Hackathon at CoSolve, Longmont CO 07-26-17

### TL;DR
```
sh install-docker.sh

```

### Docker Installation Linux
```
sh install-docker.sh
```

### Installer explained
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install -y docker-ce
```

### Other platforms
Docker for Mac
https://www.docker.com/docker-mac

Docker for Windows
https://www.docker.com/docker-windows


### Retrieve a Docker image
```
docker pull tiangolo/uwsgi-nginx-flask:flask-upload
```

### Get the Code
```
git clone https://github.com/dixon1e/internet-farm
git clone https://github.com/peterfinlan/Sedna
```

### Copy site into codebase and deploy
```
cp -R Sedna/* internet-farm/app/static
cd internet-farm
sh deploy.sh
```

### Deploy explained
```
#!/bin/bash

dockerName=api
port=8886
logging=syslog
host_share=/home/cownby/api/app
container_share=/app

docker stop $dockerName;
docker rm $dockerName;
docker rmi $dockerName;
docker build --no-cache=true -t $dockerName .;
docker run -d --name $dockerName -p $port:80 --log-driver $logging -v ${host_share}:${container_share}  $dockerName
```

### The Dockerfile
```
FROM tiangolo/uwsgi-nginx-flask:flask-upload

COPY ./app /app
```
