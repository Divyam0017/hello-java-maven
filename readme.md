Task 8: Jenkins + Maven Build
This project demonstrates Continuous Integration with Jenkins using a Java + Maven project. The pipeline pulls code from GitHub, builds the project with Maven, and verifies that the Java application runs successfully.
Project Structure
hello-java-maven/
│── pom.xml
│── Jenkinsfile
└── src/
    └── main/
        └── java/
            └── HelloWorld.java
Steps Performed
1. Create Java + Maven Project
Wrote a simple HelloWorld.java app:
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}
Defined pom.xml with maven-compiler-plugin for Java 8.
2. Build with Maven
Run the following commands:
mvn clean package
Maven compiles the app and generates a JAR in target/hello-1.0.jar.
Verified locally using:
java -cp target/hello-1.0.jar HelloWorld
3. Setup Jenkins in Docker
docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
Installed Maven Plugin inside Jenkins.
Configured Maven tool (v3.9.11).
4. Jenkins Pipeline (Jenkinsfile)
pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Divyam0017/hello-java-maven.git'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Run App') {
            steps {
                sh 'java -cp target/hello-1.0.jar HelloWorld'
            }
        }
    }
}
5. Run Pipeline
Triggered Jenkins pipeline.
Console Output showed:
Hello, Jenkins + Maven!

This confirms Jenkins successfully built and ran the Java app via Maven.
Key Learnings
- How to configure Jenkins with Maven.
- Writing a simple Jenkinsfile for build automation.
- Running a Java application as part of a Jenkins pipeline.
