Yes, absolutely. Providing links to the individual microservice repositories is the **best practice** and exactly what a recruiter or another developer would want to see. It keeps your main "guide" repository clean while allowing deep dives into the specific code of each service.

Here is the final, comprehensive `README.md` file for your central repository. You can copy and paste this directly into your `README.md` file on GitHub.

-----

# Quiz Application - A Microservices Project

Welcome to the central repository for my Quiz Application, a project built using a modern microservice architecture. This repository serves as a comprehensive guide to understand the project's structure, set up the environment, and run the entire application.

The source code for each microservice is maintained in its own individual repository, linked below.

## Project Overview

This application is a dynamic quiz platform designed with a decoupled and scalable architecture. It demonstrates key cloud-native principles, including service discovery with Eureka, a centralized API Gateway for routing, and inter-service communication using OpenFeign.

### Architecture

The application is composed of four primary microservices that work together to provide the full functionality:

```

```



  * **Service Registry (`registry-service`)**: Utilizes Netflix Eureka to allow services to register themselves and discover others. This is the central hub for our service-to-service communication network.
  * **API Gateway (`api-gateway`)**: The single entry point for all client requests. It intelligently routes traffic to the appropriate microservice and is configured to work with the service registry for dynamic routing.
  * **Question Service (`question-service`)**: Manages the lifecycle of quiz questions. It provides CRUD operations and logic for generating quizzes and calculating scores, connecting to its own MongoDB database for persistence.
  * **Quiz Service (`quiz-service`)**: Handles the creation and submission of quizzes. It communicates with the `question-service` via a declarative Feign client to fetch questions and submit answers for scoring.

### Technology Stack

  * **Backend**: Java 17, Spring Boot 3
  * **Microservices**: Spring Cloud, Netflix Eureka (Service Discovery), Spring Cloud Gateway, OpenFeign (REST Client)
  * **Database**: MongoDB
  * **Build Tool**: Maven

## Microservice Repositories

Here are the links to the public GitHub repositories for each individual microservice:

  * **Service Registry**: https://github.com/kundan424/registry-service
  * **API Gateway**: https://github.com/kundan424/api-gateway
  * **Question Service**: https://github.com/kundan424/question-service
  * **Quiz Service**: https://github.com/kundan424/quiz-service

## Getting Started

### Prerequisites

To run this application, you will need the following installed on your machine:

  * Java 17 or later
  * Apache Maven
  * A running MongoDB instance (either local or on a cloud service like MongoDB Atlas)

### How to Run the Application

1.  **Clone each microservice repository** from the links provided above.
2.  **Configure MongoDB:** In both the `question-service` and `quiz-service`, update the `src/main/resources/application.yml` file with your MongoDB URI.
3.  **Start the services in the following order:** This is critical for the services to register and discover each other correctly.
    1.  `registry-service`
    2.  `api-gateway`
    3.  `question-service`
    4.  `quiz-service`
4.  For each service, navigate to its root directory in a new terminal window and run the Spring Boot application using Maven:
    ```bash
    mvn spring-boot:run
    ```

Once all services are running without errors, the application will be fully functional and ready for requests.

## API Endpoints

All requests should be made through the **API Gateway**, which runs on `http://localhost:8080`.

#### Question Service (Routed via `/question`)

  * `GET /question/allQuestions`: Fetches all questions from the database.
  * `POST /question/add`: Adds a new question to the database.
  * `GET /question/generate`: Generates a new quiz with a specified number of questions and category.
  * `POST /question/getQuestions`: Gets the specific questions for a given quiz ID.
  * `POST /question/getScore`: Calculates the score for a submitted quiz.

#### Quiz Service (Routed via `/quiz`)

  * `POST /quiz/create`: Creates a new quiz.
  * `GET /quiz/get/{id}`: Retrieves a specific quiz for a user to take (questions only, no answers).
  * `POST /quiz/submit/{id}`: Submits user responses for a quiz and returns the final score.

*For detailed request/response examples, please see the `README.md` files in the individual service repositories.*