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
        //sh '/usr/bin/docker build -t bank-customer-service .'
       sh '/usr/bin/docker build -t myrepo .'
      }
    }
    stage('Push image') {
      steps {
        //withDockerRegistry([credentialsId: 'sri556', url: "https://index.docker.io/v1/"]) {
        //withDockerRegistry(credentialsId: 'sri556', url: 'https:// 4f45d219f3d9.dkr.ecr.ap-south-1.amazonaws.com/sri556') {
          //sh '/usr/bin/docker tag  bank-customer-service sri556/bankrepo:latest'
          //sh '/usr/bin/docker push sri556/bankrepo:latest'
          docker.withRegistry('https://651843681614.dkr.ecr.ap-south-1.amazonaws.com', 'ecr:ap-south-1:demo-ecr-credentials') {  docker.image('bankrepo').push('latest')   }

         //withDockerRegistry(credentialsId: 'ecr:ap-south-1:mycredentials', url: 'https://651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo') {
          sh 'docker tag myrepo:latest 651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo:latest:v2'
          sh 'docker push 651843681614.dkr.ecr.ap-south-1.amazonaws.com/myrepo:latest:v2'
        }
      }
    }
  }
  
  

