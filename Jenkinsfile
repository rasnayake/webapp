pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage ('Build') {
      steps {
      sh "mvn clean package" 
      }
    }
        stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'sudo scp -o StrictHostKeyChecking=no target/*.war tsroot@137.135.120.26:/prod/apache-tomcat-8.5.54/webapps/webapp.war'
              }      
           } 
    }
  }
  }

