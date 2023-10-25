# Task Manager

Multi-user task scheduler. Users can use it as a TODO-list. Project with microservice architecture.

## Stack
* Java, Kotlin
* Maven
* Spring Boot, Spring Security, Spring Session, Spring AMQP, Spring Scheduler, Spring Mail
* PostgreSQL, Spring Data JPA
* Docker
* Message BrockerRabbitMQ - Queues
* CI/CD
A microservice approach was used in the project development. The project includes 3 microservices:


## [Backend](https://github.com/sh1neqd/task-manager-backend "Backend")
Spring Boot application that implements a REST API to work with users, jwt token created during authorization and tasks.

Working with users:

* Registration
* Authorization
* Logout

Working with tasks:

* Create, edit (each task has a title and description)
* Marking a task as done
* Deleting

## [Email sender](https://github.com/sh1neqd/task-manager-emailsender "Email sender")
Spring Boot application with two modules - Spring Mail and Spring AMQP.

With Spring AMQP, the application connects to RabbitMQ and creates a message queue, then subscribes to messages received from the scheduler and backend service.

For each message received, whose contents are deserialized into a model instance, the Spring Mail module is used to send an email to the user's email address

## [Scheduler](https://github.com/sh1neqd/task-manager-scheduler "Scheduler")

Spring Boot application with two modules - Spring Scheduler and Spring AMQP.

The task of the service is to iterate all users once a day, generate reports for them about tasks and changes in them for a day, and generate emails for sending. The generated emails are sent to the RabbitMQ queue.
