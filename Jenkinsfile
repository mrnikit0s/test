pipeline {
    agent{
        label "jenkins-agent"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    } 
    stages{
      stage ('A') {
        steps {
            sh 'mvn --version'
        }
      }
    }
}