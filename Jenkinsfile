pipeline {
    agent any
    environment {
      PATH = "/usr/share/apache-maven/bin:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64:$PATH"
    }
    
    stages {
        stage ('build') {
            steps {
                sh "mvn clean test package"
            }
        }
        stage ('analysis') {
            steps {
              withSonarQubeEnv('sonarqube'){
                sh "mvn sonar:sonar"
              }
            }
      }
    }
  }
