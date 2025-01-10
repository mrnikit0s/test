pipeline {
    agent{
        label "jenkins-agent"
    }
    tools{
        jdk 'Java17'
        maven 'Maven3'
    } 
    environment {
        APP_NAME = "complete-prodcution-e2e-pipeline"
        RELEASE = "1.0.0"
        DOCKER_USER = "mrnikit0s"
        DOCKER_PASS = 'dockerhub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${env.BUILD_NUMBER}"
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
      stage('Quality Gate') {
        steps {
            waitForQualityGate(abortPipeline: false, credentialsId: 'sonar-new')
        }
      }
    }
      
}