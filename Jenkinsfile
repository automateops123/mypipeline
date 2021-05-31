pipeline {
    agent any
    environment {
      PATH = "/usr/share/apache-maven/bin:/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.amzn2.0.1.x86_64:$PATH"
    }
    
    stages {
        
        stage ('deploy') {
            steps {
              sshagent(['deployuser']) {
                    sh '''
                    ssh ec2-user@172.31.59.4
                    sudo touch /home/ec2-user/Dockerfile
                    sudo chown ec2-user:ec2-user /home/ec2-user/Dockerfile
                    cat > /home/ec2-user/Dockerfile <<EOL
                    FROM tomcat:latest
                    COPY ./webapp.war /usr/local/tomcat/webapps
                    RUN cp -r /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps
                    EOL
                    sudo docker build -t customimage .
                    docker run -d -p 8080:8080 --name customcontainer customimage
                    '''
                }
              }
            }
      }
    }
  
