pipeline {
    agent any
    environment {
      PATH = "/usr/share/apache-maven/bin:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64:$PATH"
    }
    
    stages {
        
        stage ('deploy') {
            steps {
              sshagent(['deployuser']) {
                    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/mypipeline1/webapp/target/webapp.war ec2-user@ip-172-31-18-126:/home/ec2-user"
              }
            }
      }
    }
}
  
