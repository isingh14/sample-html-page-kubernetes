pipeline {
     agent any
     triggers {
          pollSCM('* * * * *')
     }
     stages {
     	  stage("Docker build") {
               steps {
                    sh "docker build -t isingh14/sample-html:${BUILD_TIMESTAMP} ."
               }
          }

          stage("Docker login") {
               steps {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'docker-hub-credentials',
                               usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
                         sh "docker login --username $USERNAME --password $PASSWORD"
                    }
               }
          }

          stage("Docker push") {
               steps {
                    sh "docker push isingh14/sample-html:${BUILD_TIMESTAMP}"
               }
          }

          stage("Update version") {
               steps {
                    sh "sed  -i 's/{{VERSION}}/${BUILD_TIMESTAMP}/g' static-web-deployment.yaml"
               }
          }
          
          stage("Deploy to staging") {
               steps {
                    sh "kubectl apply -f static-web-deployment.yaml"
               }
          }
     }
}

