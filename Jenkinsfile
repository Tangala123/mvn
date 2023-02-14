pipeline {
   agent any
  stages {
    stage ("Git Checkout") {  
      steps {
           git branch: 'main', credentialsId: 'git', url: 'https://github.com/Tangala123/mvn'
      }
    }
    stage ("Maven Build") {
      steps {
        sh "mvn clean package"
      }  
    }
    stage ("Tomcat Deploy") {
      steps {
        sshagent(['creds']) {
          sh "scp -o strictHostKeyChecking=no target/*.war ec2-user@172.31.15.62:/opt/tomcat01/webapps"
          sh "ssh ec2-user@172.31.15.62 /opt/tomcat01/bin/shutdown.sh"
          sh "ssh ec2-user@172.31.15.62 /opt/tomcat01/bin/startup.sh"
        }
      }  
    }
  }
}
