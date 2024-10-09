pipeline {
  agent any
     tools {
       maven 'M2_HOME'
           }
 
  stages {
    stage('Git Checkout') {
      steps {
        echo 'This stage is to clone the repo from github'
        git branch: 'master', url: 'https://github.com/rakesh1050/star-agile-health-care.git'
                        }
            }
    stage('Create Package') {
      steps {
        echo 'This stage will compile, test, package my application'
        sh 'mvn package'
                          }
            }
    stage('Generate Test Report') {
      steps {
        echo 'This stage generate Test report using TestNG'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Healthcare/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                          }
            }
    stage('Create Docker Image') {
      steps {
        echo 'This stage will Create Docker image'
        sh 'docker build -t rakesh1050/Healthcare:1.0'
                          }
            }
    stage('Login to Dockerrhub') {
      steps {
        echo 'This stage will loginto Dockerhub'
        withCredentials([usernamePassword(credentialsId: 'Dockerlogin', passwordVariable: 'docker-pass', usernameVariable: 'docker-login')]) {
        sh 'docker login -u ${docker-login} -p${docker-pass}'
        }
      }
    }
    stage('Docker Push-Image') {
      steps {
        echo 'This stage will push my new image to the dockerhub'
        sh 'docker build -t rakesh1050/Healthcare:1.0'
          }
    }
  } 
}  
    
