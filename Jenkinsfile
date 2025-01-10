pipeline {
    agent{
        label "jenkins-agent"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    } 
    stages{
      stage ('Cleanup Workspace') {
        steps {
            cleanWs()
        }
      }

      stage ('Chekout from SCM') {
        steps {
            git branch: 'main', credentialsId: 'github', url: 'https://github.com/mrnikit0s/test'
        }
      }

      stage ('Build Application') {
        steps {
            sh "mvn clean -X"
        }
      }

      stage ('Test Application') {
        steps {
            sh "mvn test"
        }
      }

      stage ('Sonarqube Analysis ') {
        steps {
            withSonarQubeEnv(credentialsId: 'sonar-new', installationName:'sonarqube')   {
                sh "mvn sonar:sonar"
            }   
        }
      }
    }
      
}