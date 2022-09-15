pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-id', url: 'https://github.com/etechDevops/etech-mavenApp.git']]])
      }
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage ('codequality'){
      steps{
        sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team3-pipeline \
  -Dsonar.host.url=http://ec2-52-87-202-212.compute-1.amazonaws.com:9000 \
  -Dsonar.login=sqp_8a6bfdd291c85d54ca9b9ee1757367bd1015a13e'
      }
    }
    stage('unittest'){
        steps{
            sh 'mvn test'
      }
    }
  }
}
