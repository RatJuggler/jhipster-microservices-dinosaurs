# JHipster generated Docker-Compose configuration

## Usage

Launch all your infrastructure by running: `docker-compose up -d`.

## Configured Docker services

### Service registry and configuration server:

- [Consul](http://localhost:8500)

### Applications and dependencies:

- catalogue (microservice application)
- catalogue's mysql database
- catalogue's elasticsearch search engine
- game (microservice application)
- game's mysql database
- gateway (gateway application)
- gateway's mysql database
- gateway's elasticsearch search engine
- sighting (microservice application)
- sighting's mongodb database
- sighting's elasticsearch search engine

### Additional Services:

- Kafka
- Zookeeper
- [JHipster Console](http://localhost:5601)
- [Zipkin](http://localhost:9411)
