pipeline {
    agent any
    
    stages {
        stage("compile code") {
            steps {
                checkout scm
            }
            steps{
              sh 'java -version'
					    sh 'jar -cvf SWE645HW1P2.war *'
            }
        }
        
        stage("Docker Ops") {
            steps {
                script {
                    ourapp = docker.build("krishnamandanapu/ss:${env.BUILD_ID}")
                }
            }
            steps {
                script {
                	sh 'docker login -u krishnamandanapu -p Kri$hn@1234'
					        ourapp.push("${env.BUILD_ID}")
                }
            }
        }
                
        stage("UpdateDeployment") {
          steps{
            sh 'kubectl config view'
            sh "kubectl get deployments"
            sh "kubectl set image deployment/hw2dep container-0= krishnamandanapu/ss:${env.BUILD_ID}"
          }
		    }
    }    
}
