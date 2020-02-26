# jhipster-microservices-dinosaurs

This is the parent sandbox for a suite of [JHipster](https://www.jhipster.tech/) generated microservice applications to play around 
with and deploy to various cloud providers and containers.

It includes:
- [Gateway Application](https://github.com/RatJuggler/jhipster-microservices-dinosaurs-gateway)
- [Dinosaur Catalogue Microservice](https://github.com/RatJuggler/jhipster-microservices-dinosaurs-catalogue)
- [Dinosaur Game Backend Microservice](https://github.com/RatJuggler/jhipster-microservices-dinosaurs-game)
- [Dinosaur Sighting Microservice](https://github.com/RatJuggler/jhipster-microservices-dinosaurs-sighting)

As the diagram indicates this results in a fair few docker containers to run (20) so if you are going to run everything locally make 
sure that you have plenty of memory / swap space free. I was able to run everything on an i7 laptop using Ubuntu MATE 18.04 LTS with 
16GB memory and 16GB swap space.

![Image of Services](https://raw.githubusercontent.com/RatJuggler/jhipster-microservices-dinosaurs/master/jhipster-microservices.png)

## Generation

The gateway and microservices were all generated from a single [jdl](https://www.jhipster.tech/jdl/) 
[file](https://github.com/RatJuggler/jhipster-jdl/blob/master/jhipster-microservices-dinosaurs.jh) using the following commands:

    mkdir jhipster-microservices-dinosaurs
    cd jhipster-microservices-dinosaurs
    jhipster import-jdl jhipster-microservices-dinosaurs.jh

The individual components were committed to git as submodules with this project as the parent.

Currently using JHipster [6.7.1](https://www.jhipster.tech/documentation-archive/v6.7.1).

## Deployments

The following deployments have been tested for this version of the application.

### Docker

Following [these](https://www.jhipster.tech/docker-compose/) instructions. We first need to create a docker image for each 
application which can then be pushed to docker hub if required:

    cd <application>
    ./mvnw -Pprod -DskipTests verify jib:dockerBuild
    docker tag <image-id> <dockerRepositoryName>/<application>:latest
    docker push <dockerRepositoryName>/<application>:latest

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
    <not selected>
    ? Do you want to setup monitoring for your applications ? 
    Yes, for logs and metrics with the JHipster Console (based on ELK and Zipkin)
    ? You have selected the JHipster Console which is based on the ELK stack and additional technologies, which one do you want to use ?
    Curator, to help you curate and manage your Elasticsearch indices, 
    Zipkin, for distributed tracing (only compatible with JHipster >= v4.2.0)

To bring everything up you'll need to use:

    docker-compose up -d

After that you can control the services using commands:

    docker-compose stop

    docker-compose start

An environment file (.env) can remove the need to keep specifying file and project options.
