# the-voting-app

Example voting app (DockerConf EU 2015)  

The original demo was designed to run on top of a `Swarm` scheduler with `docker compose`.  
This one has been modified to run on top of a `Marathon/Mesos` scheduler.  

Five docker containers are used to compose the product platform:

- docker-tva-postgres
- docker-tva-redis
- docker-tva-results
- docker-tva-voting
- docker-tva-worker

#### clone

This is the control repository. A recursive Git clone is needed in order to pull all Git submodules:

```
git clone --recursive ${GIT_SERVER_URL}/the-voting-app.git
cd the-voting-app && git submodule foreach 'git checkout master'
```
