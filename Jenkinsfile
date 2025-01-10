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
            sh "mvn clean package"
        }
      }

      stage ('Test Application') {
        steps {
            sh "mvn test"
        }
      }

      stage ('Sonarqube Analysis ') {
        steps {
            def scannerHome = tool 'SonarScanner 4.0';
            withSonarQubeEnv(credentialsId: 'sonar', installationName:'sonar')   {
                sh "mvn sonar:sonar"
            }   
        }
      }
    }
      
}