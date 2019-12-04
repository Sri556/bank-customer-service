pipeline {
  agent any
  tools { 
        maven 'Maven3'
        jdk 'jdk'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    stage('Docker Build') {
      steps {
        sh '/usr/bin/docker build -t bank-customer-service .'
      }
    }
    stage('Push image') {
      steps {
        withDockerRegistry([credentialsId: 'sri556', url: "https://index.docker.io/v1/"]) {
        //withDockerRegistry(credentialsId: 'sri556', url: 'https:// 4f45d219f3d9.dkr.ecr.ap-south-1.amazonaws.com/sri556') {
          sh '/usr/bin/docker tag  bank-customer-service sri556/bankrepo:latest'
          sh '/usr/bin/docker push sri556/bankrepo:latest'
        // withDockerRegistry(credentialsId: 'ecr:ap-south-1:mycredentials', url: 'http://118463809662.dkr.ecr.ap-south-1.amazonaws.com/myrepo') {
          //sh 'docker tag sri556/bank-customer-service:latest 118463809662.dkr.ecr.ap-south-1.amazonaws.com/myrepo:v2'
          //sh 'docker push 118463809662.dkr.ecr.ap-south-1.amazonaws.com/myrepo:v2'
        }
      }
    }
  }
  
  
}
