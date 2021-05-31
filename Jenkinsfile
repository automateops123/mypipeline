pipeline {
    agent any
    environment {
      PATH = "/usr/share/apache-maven/bin:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64:$PATH"
    }
    
    stages {
        
        stage ('deploy') {
            steps {
              sshagent(['deployuser']) {
                    sh 'scp -o StrictHostKeyChecking=no Dockerfile ec2-user@172.31.59.4:/home/ec2-user'
                    sh 'docker build -t customimage .'
                    sh 'docker run -d -p 8080:8080 --name customcontainer customimage'
                     }
              }
        }
      }
    }
  
