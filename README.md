# dhis-docker
Running dhis2 on docker

1. Clone the repo to your local machine. *git clone https://github.com/lmphatsi/dhis-docker.git*
2. Open the docker-compose file and specify the dhis2 version you'd prefer to run.
3. Place your postgres db dump in **config** folder. Alternatively you can grab a sample dump here: https://databases.dhis2.org/ and rename it to **init.sql**. Ensure that the db dump schema version and dhis2 version match. 
4. Fire up the containers using - docker-compose up -d. This will spin up two docker containers - dhis-docker_db (with postgres pre-populated with the dump specified above) and dhis-docker)web (with tomcat and the dhis2 web app)
5. Go to localhost:8080 or *Machine_IP*:8080
