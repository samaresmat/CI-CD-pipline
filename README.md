# CI/CD Pipeline with Jenkins, Docker, and Spring Boot

## Project Overview

This project demonstrates a complete CI/CD pipeline using Jenkins, Docker, GitHub, and Spring Boot.

The pipeline performs the following tasks:

1. Build the application using Maven.
2. Run automated tests.
3. Create a Docker image.
4. Deploy the application as a Docker container.

---

## Technologies Used

- Java 17
- Spring Boot
- Maven
- Jenkins
- Docker
- GitHub

---

## Project Structure

```text
helloapp
│
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com/demo/helloapp
│   │   │       ├── HelloappApplication.java
│   │   │       └── HelloController.java
│   │   │
│   │   └── resources
│   │
│   └── test
│
├── Dockerfile
├── Jenkinsfile
├── pom.xml
└── README.md
```

---

## Application Endpoint

The application provides a simple REST endpoint:

```http
GET /
```

Response:

```text
Hello Jenkins and Docker
```

---

## HelloController

```java
package com.demo.helloapp;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/")
    public String home() {
        return "Hello Jenkins and Docker";
    }
}
```

---

## Build the Application

Run the following command:

```bash
mvn clean package
```

Generated JAR file:

```text
target/*.jar
```

---

## Docker Configuration

### Dockerfile

```dockerfile
FROM eclipse-temurin:17-jre

COPY target/*.jar app.jar

ENTRYPOINT ["java","-jar","/app.jar"]
```

### Build Docker Image

```bash
docker build -t helloapp .
```

### Run Docker Container

```bash
docker run -d -p 8080:8080 helloapp
```

---

## Jenkins Pipeline

### Jenkinsfile

```groovy
pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t helloapp .'
            }
        }

        stage('Deploy') {
            steps {
                bat 'docker run -d -p 8080:8080 helloapp'
            }
        }
    }
}
```

---

## CI/CD Workflow

```text
GitHub
   ↓
Jenkins Pipeline
   ↓
Build
   ↓
Test
   ↓
Docker Build
   ↓
Deploy Container
```

---



