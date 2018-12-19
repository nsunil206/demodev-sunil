pipeline {
    agent {label 'jenkins_dev_dcos' }
    environment {
        GIT_SHA_SHORT="${GIT_COMMIT[0..6]}"
    }

    stages {
      stage('Checking out demo-common') {
        steps {
            sh 'mkdir -p demo-common'
             dir('demo-common'){
               sh """ https://github.com/nsunil206/demo-common.git """
               echo "Building demo-common"
               sh 'mvn clean install'
            }
            
        }
      }
        stage('Checking demo-test') {
           steps {
            sh 'mkdir -p demo-test' 
              dir('demo-test'){
               sh """ https://github.com/nsunil206/demo-test.git """
               echo "BUilding demo-test"
               sh 'mvn clean install'
            }
           
        }
      }
        stage('BUILD') {
        steps {
          echo "Git commit sha is ${GIT_SHA_SHORT}"
          
          echo "Building the code"
        }
      }
      stage('INTEGERATION TEST') {
        steps {
            sh 'echo "run integeration tests here"'
        }
      }
      stage('DOCKER BUILD') {
        steps {
              echo "docker build"
              
              sh '''
         sudo docker build -t incxregistry.incx-dev.io/incx_dev/test:${GIT_SHA_SHORT} .
         sudo docker push incxregistry.incx-dev.io/incx_dev/test:${GIT_SHA_SHORT}
      '''
          }
        }
   
    stage('marathon deploy') {
        steps {
              echo "marathon deploy"
             }
         }
    }
 }
   
