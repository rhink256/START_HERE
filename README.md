# START_HERE
Temperature Monitoring Project Description

## Overview

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

## Automation

It doesn't completely come across in the github version of the project as it is not integrated with my local infrastructure, but this product demonstrates complete build, test, and deployment automation using Jenkins and Docker. The Jenkinsfiles and Dockerfiles are visible, but to get this completely working you would need an instance of Jenkins, a maven artifact repository, and a docker repository, and Gitlab (or similar) with webhooks configured to trigger Jenkins builds. Further, Jenkins would need to be configured with user credentials for the maven and docker repositories.

## Components

The runtime components of this system are:

- Client (Javascript / Vue / VueX / Vuetify, served by Node.js, running in a Docker container)
- Server (Java EE / Hibernate, served by Wildfy, running in a Docker container)
- Environmental Sensors (Arduino

## Limitations

This project is a work in progress and not without warts. Some of the dependencies are out of date, the front end has no unit tests and there are unit tests missing for some classes in the back end. There is also absolutely no user management or authentication.
