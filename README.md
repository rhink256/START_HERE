# Temperature Monitoring Project Description

## Overview

A real-time logging temperature and humidity monitoring platform. It supports as many external sensors as you like, and can read data from local National Weather Service stations using their public [API](https://www.weather.gov/documentation/services-web-api).

The following image shows the client as rendered in a mobile web browser, with two sensors and one national weather service source.

<img src="signal-2022-06-20-140959.jpg" width="200"/>

This is a learning project I began to teach myself new techologies and platforms, and do something useful at the same time. Overall the project is not terribly complex but demonstrates the integration of a number of real world technologies. The intent is to create a product stack that would be suitable for real world use. The technologies and products used include:

- Docker
- Docker compose
- Docker networking
- Jenkins
- Nexus
- Vue 2
- VueX
- Vuetify
- Node.js
- Javascript
- Java
- Java Enterprise Edition
- Java Persistence API (JPA) / Hibernate
- Arduino Embedded Development (C++)
- Gradle
- REST API's (including using public APIs and creating my own)
- Javascript Object Notation (JSON)
- Wildfly/JBOSS
- H2 in memory database (for unit testing of database queries)

## Repositories

- [Server](https://github.com/rhink256/temperature_server)
- Client
- [Sensor](https://github.com/rhink256/arduino_sensor)
- Compose
- Server Container Image: Wildfly + Postgres Driver
- Test Scripts

## Automation

It doesn't completely come across in the github version of the project as it is not integrated with my local infrastructure, but this product demonstrates complete build, test, and deployment automation using Jenkins and Docker. The Jenkinsfiles and Dockerfiles are visible, but to get this completely working you would need an instance of Jenkins, a maven artifact repository, and a docker repository, and Gitlab (or similar) with webhooks configured to trigger Jenkins builds. Further, Jenkins would need to be configured with user credentials for the maven and docker repositories.

## Components

### Client

The client is a Javascript based web front end built on top of the Vue framework. It uses VueX for state management and Vuetify for components. It communicates with the server via Websockets and REST.

It is served by Node.js running in a Docker container.

### Server

The server is built on Java Enterprise Edition. It uses Hibernate as its JPA provider. It communicates with the Client as described above. It runs on the Wildfly application server, running in a Docker container. The Docker container is customized with the postgres JDBC driver.

### Database

An unmodified postgres docker image, configured and run thusly: 
```
docker run \
    --name temperature_database_postgres \
    -p 192.168.1.207:5432:5432 \
    -e POSTGRES_PASSWORD=[PASSWORD] \
    -v temperature_database:/var/lib/postgres/data \
    --restart always \
    -d postgres
```

### Environmental Sensors

This can be anything sending the appropriate JSON to the appropriate REST endpoint. My implementation is the Arduino [MKR-WIFI-1010](https://store-usa.arduino.cc/products/arduino-mkr-wifi-1010?selectedStore=us) with the [MKR Env Shield](https://store.arduino.cc/collections/sensors-environment/products/arduino-mkr-env-shield-rev2). The implementation is optimized for battery life; with the board LED's removed it'll run for about 2 months with 3000 mAh Lithium Ion battery. It wakes up from deep sleep every 15 minutes, reads its sensors, transmits them to the server via WIFI, and goes back into deep sleep.

The server can handle input from any number of sensors; they are distinguished by their IP address.

## Limitations

This project is a work in progress and not without warts. These include but are not limited to the following:

Some of the dependencies are out of date, the front end has no unit tests and there are unit tests missing for some classes in the back end. There is also absolutely no user management or authentication.

The National Weather Service client is currently hardcoded. You would have to change the station identifier in the REST endpoint URL to change the station.

The websocket implementation is naive; it currently has no ability to reconnect on connection failure without refreshing the page.
