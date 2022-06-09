# dhis-docker

<h1>DHIS2 on docker</h1>
This repo contains a number of docker-compose files to help spin up dockerised dhis2 setups with ease. 
<h2>A. Setting up a training instance</h2>
Assuming you have installed docker and docker-compose on your host machine, follow the steps below. 
<ol>
<li>
  Get the dump here: <pre><code>https://thuto.nul.ls/pt/dhis_db_backup_228_07_06_2022_02_10_01.sql.gz</code></pre>
  De-compress it: <pre><code>gzip -d dhis_db_backup_228_07_06_2022_02_10_01.sql.gz</code></pre>
</li>
<li>Clone this repo.<pre><code>git clone https://github.com/lmphatsi/dhis-docker.git</code></pre></li>
<li>Navigate to the dhis-docker directory<pre><code>cd dhis-docker</code></pre></li>
<li>Edit the docker-compose file (docker-compose-training-live-db.yml) in accordance to the location of the db dump. -- see volumes under the *db* container service</li>
<li>Launch the base dhis2 setup. This will spin up two containers: dhis-docker_web and dhis-docker_db. <pre><code>docker-compose -f docker-compose-training-live-db.yml up</code></pre></li>
<li>When both containers are up, a base dhis2 instance should be accessible at: <pre><code>http://localhost:8080</code></pre></li>
<li>Go into the db container and create a role and an empty database.
<pre><code>docker exec -it dhis-docker_db_1 bash</code></pre>
<pre><code>psql -U postgres</code></pre>
<pre><code>CREATE DATABASE dhis_lsmoh_235_8;</code></pre>
<pre><code>CREATE ROLE dhis WITH SUPERUSER;</code></pre>
Quit: <pre><code>\q</code></pre>
</li>
<li>Restore the db dump into the empty dhis db
<pre><code>psql -U postgres dhis_lsmoh_235_8 < /festere/dhis_db_backup_228_07_06_2022_02_10_01.sql</code></pre>
And wait ... or better yet, grab a cup of coffee.

</li>
<li>After a successful db restore, stop the containers and point the dhis2 web app to the new database - dhis_lsmoh_235_8
  <pre><code>docker-compose stop</code></pre>
  Update the dhis.conf file <pre><code>nano ./config/dhis2_home/dhis.conf</pre></code> : <pre><code>connection.url = jdbc:postgresql://db/dhis_lsmoh_235_8</code></pre>
  Startup the containers<pre><code>docker-compose -f docker-compose-training-live-db.yml up</code></pre>
</li>



<h2>B. Other (this part is yet to be updated)</h2>
Running dhis2 on docker

1. Clone the repo to your local machine. _git clone https://github.com/lmphatsi/dhis-docker.git_
2. Open the docker-compose file and specify the dhis2 version you'd prefer to run.
3. Make changes to the **config/dhis2_home/dhis.conf** file. e.g. setting a strong password _(Optional if this is for testing purposes)_
4. Place your postgres db dump in **config** folder. Alternatively you can grab a sample dump here: https://databases.dhis2.org/ and rename it to **init.sql**. Ensure that the db dump schema version and dhis2 version match.
5. Fire up the containers using - docker-compose up -d. This will spin up two docker containers - dhis-docker_db (with postgres pre-populated with the dump specified above) and dhis-docker)web (with tomcat and the dhis2 web app)
6. Go to localhost:8080 or _Machine_IP_:8080 and voila!!!
