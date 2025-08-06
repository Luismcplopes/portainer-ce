# portainer-ce
How to run portainer-ce

## Run it docker-compose 

```shell
> git@github.com/luislopescmc/portainer-ce.git
> cd portainer-ce
> docker-compose up -d
```

## docker run
```
$ docker volume create portainer_data
$ docker run -d -p 8000:8000 -p 9443:9443 --name portainer --restart=always \
 -v /var/run/docker.sock:/var/run/docker.sock \
 -v portainer_data:/data portainer/portainer-ce:lts
```


https://docs.portainer.io/start/install-ce/server/docker/linux
https://earthly.dev/blog/portainer-for-docker-container-management
https://docs.portainer.io/start/install-ce/server/docker/linux


## Resetting Admin password in Portainer running as container

https://omar2cloud.github.io/rasp/psswd/

docker container stop portainer
docker run --rm -v portainer_data:/data portainer/helper-reset-password

2020/06/04 00:13:58 Password succesfully updated for user: admin
2020/06/04 00:13:58 Use the following password to login: &_4#\3^5V8vLTd)E"NWiJBs26G*9HPl1

docker container start portainer


## Updating your Portainer Server

docker stop portainer
docker rm portainer
docker pull portainer/portainer-ce:latest
docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest


## Agent-only upgrade

docker stop portainer_agent
docker rm portainer_agent
docker pull portainer/agent:latest
docker run -d -p 9001:9001 --name portainer_agent --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/docker/volumes:/var/lib/docker/volumes portainer/agent:latest



If you have set a custom AGENT_SECRET on your Portainer Server instance (by specifying an AGENT_SECRET environment variable when starting the Portainer Server container) you must remember to explicitly provide the same secret to your Agent in the same way (as an environment variable) when updating your Agent:
-e AGENT_SECRET=yoursecret
