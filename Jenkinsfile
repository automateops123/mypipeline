pipeline {
    agent any
    environment {
      PATH = "/usr/share/apache-maven/bin:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64:$PATH"
    }
    
    stages {
        
        stage ('deploy') {
            steps {
              sshagent(['deployuser']) {
                    sh script: '''
                    touch dockerfile
                    cat <<EOT>>dockerfile
                    FROM tomcat:latest
                    COPY ./webapp.war /usr/local/tomcat/webapps
                    RUN cp -r /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps
                    EOT
                    sudo docker build -t webimage .
                    sudo docker run -d -p 8080:8080 --name mycontainer webimage'''
              }
            }
      }
    }
}
  
