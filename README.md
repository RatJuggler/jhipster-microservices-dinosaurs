# jhipster-microservices-dinosaurs

This is the parent sandbox for a suite of [JHipster](https://www.jhipster.tech/) generated microservice applications to play around 
with and deploy to various cloud providers and containers.

Currently using JHipster [6.7.1](https://www.jhipster.tech/documentation-archive/v6.7.1).

## Generation

The gateway and microservices were all generated from a single [jdl](https://www.jhipster.tech/jdl/) 
[file](https://github.com/RatJuggler/jhipster-jdl/blob/master/jhipster-microservices-dinosaurs.jh) using the following commands:

    mkdir jhipster-microservices-dinosaurs
    cd jhipster-microservices-dinosaurs
    jhipster import-jdl jhipster-microservices-dinosaurs.jh

The individual components were committed to git as submodules with this project as the parent.

## Deployments

The following deployments have been tested for this version of the application.

### Docker

Following [these](https://www.jhipster.tech/docker-compose/) instructions we can create a docker image for each application and 
push it to docker hub:

    cd <application>
    ./mvnw -Pprod -DskipTests verify jib:dockerBuild
    docker tag <image-id> johnchase/<application>:latest
    docker push johnchase/<application>:latest

You can then still run up local instances of the individual applications and their required services (see each application for 
details) but for this parent project we are interested in looking at the orchestration of the complete suite of applications. To do 
this we should generate a global Docker Compose configuration using the following:

    mkdir docker-compose
    cd docker-compose
    jhipster docker-compose

Answer the questions and add ELK as a monitoring solution to generate the configuration. 

    ? Which *type* of application would you like to deploy? 
    Microservice application
    ? Which *type* of gateway would you like to use? 
    JHipster gateway based on Netflix Zuul
    ? Enter the root directory where your gateway(s) and microservices are located ../
    4 applications found at /home/john/IdeaProjects/jhipster-microservices-dinosaurs/
    ? Which applications do you want to include in your configuration? 
    jhipster-microservices-dinosaurs-catalogue, 
    jhipster-microservices-dinosaurs-game, 
    jhipster-microservices-dinosaurs-gateway, 
    jhipster-microservices-dinosaurs-sighting
    ? Which applications do you want to use with clustered databases (only available with MongoDB and Couchbase)?
    <not seleted>
    ? Do you want to setup monitoring for your applications ? 
    Yes, for logs and metrics with the JHipster Console (based on ELK and Zipkin)
    ? You have selected the JHipster Console which is based on the ELK stack and additional technologies, which one do you want to use ?
    Curator, to help you curate and manage your Elasticsearch indices, 
    Zipkin, for distributed tracing (only compatible with JHipster >= v4.2.0)

You can then control all the services using commands as previously:

    docker-compose up -d

    docker-compose stop

    docker-compose down

Using an environment file (.env) can remove the need to keep specifying file and project options.
