pipeline{
    agent any
    tools{
       maven 'maven3'
    }
    stages{
        stage("build maven"){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/manikanta3566/spring-boot-jdocker-jenkins']]])
                sh 'mvn clean install'
            }
        }
       stage("build docker image"){
           steps{
               script{
                   sh 'docker build -t manikanta44/spring-boot-docker .'
               }
           }
       }
       stage("push docker image to docker hub"){
           steps{
               script{
                   withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                sh 'docker login -u manikanta44 -p ${dockerhubpwd}'
              }
                sh 'docker push manikanta44/spring-boot-docker'
               }
           }
       }

    }
}