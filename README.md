# dhis-docker
Dockerizing dhis2

* Place your postgres db dump in config folder and rename it to "init.sql". Alternatively you can grab a sample dump here: https://databases.dhis2.org/
Ensure that the db dump schema version and dhis2 version match.
Fire up the containers using - docker-compose up -d. This will spin up two docker containers - db (with postgres pre-populated with the dump specified above) and web (with tomcat and the dhis2 web app)
Go to localhost:8080 or *Machine_IP*:8080
