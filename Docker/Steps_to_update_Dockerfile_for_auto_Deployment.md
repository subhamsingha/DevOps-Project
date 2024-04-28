#Update Docker file to automate deployment process

# Create docker folder in /opt dir on docker host

`
cd /opt
mkdir docker
chown -R dockeradmin:dockeradmin /opt/docker
`

### Create docker file in /opt/docker folder and the copy war file to docker container

FROM tomcat:latest
RUN cp -R /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps/
COPY ./*.war /usr/local/tomcat/webapps/


### Build the Docker Image

docker build -t tomcat:v1 .

## Run the Docker Container
docker run -d --name tomcatv1 -p 8086:8080 tomcat:v1

## To access our application 
http://<public ip>:<port>/webapp


