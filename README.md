# dhis-docker

Running dhis2 on docker

1. Clone the repo to your local machine. _git clone https://github.com/lmphatsi/dhis-docker.git_
2. Open the docker-compose file and specify the dhis2 version you'd prefer to run.
3. Make changes to the **config/dhis2_home/dhis.conf** file. e.g. setting a strong password _(Optional if this is for testing purposes)_
4. Place your postgres db dump in **config** folder. Alternatively you can grab a sample dump here: https://databases.dhis2.org/ and rename it to **init.sql**. Ensure that the db dump schema version and dhis2 version match.
5. Fire up the containers using - docker-compose up -d. This will spin up two docker containers - dhis-docker_db (with postgres pre-populated with the dump specified above) and dhis-docker)web (with tomcat and the dhis2 web app)
6. Go to localhost:8080 or _Machine_IP_:8080 and voila!!!
