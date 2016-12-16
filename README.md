# the-voting-app

Example voting app (DockerConf US 2016)  

The original demo was designed to run on top of a `Swarm` scheduler with `docker compose`.  
This one has been modified to run on top of a `Marathon/Mesos` scheduler.  

Five docker containers are used to compose the product platform:

- docker-tva-postgres
- docker-tva-redis
- docker-tva-results
- docker-tva-voting
- docker-tva-worker

#### Clone

This is the control repository. A recursive Git clone is needed in order to pull all Git submodules:

```
git clone --recursive ${GIT_SERVER_URL}/the-voting-app.git
cd the-voting-app && git submodule foreach 'git checkout master'
```

#### Run

Export `MARATHON_URL` to point to your Marathon scheduler and send the task request:

```
export MARATHON_URL='http://marathon.demo.mesos:8080'
./bin/deploy
```

#### Architecture

![Architecture diagram](architecture.png)

* A Python webapp which lets you vote between two options
* A Redis queue which collects new votes
* A .NET worker which consumes votes and stores them in…
* A Postgres database backed by a Docker volume
* A Node.js webapp which shows the results of the voting in real time
