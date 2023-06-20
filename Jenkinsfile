pipeline {
  agent any

  stages {
    stage('Build & Unit test') {
      steps {
        sh 'mvn clean verify -DskipITs=true';
        junit '**/target/surefire-reports/*.xml'
        archive 'target/*.jar'
      }
    }

  stage('Static Code Analysis'){
       sh 'mvn clean verify sonar:sonar -Dsonar.projectName=DeployFront -Dsonar.projectKey=DeployFront -Dsonar.projectVersion=$BUILD_NUMBER';
    }

  stage ('Integration Test'){
       sh 'mvn clean verify -Dsurefire.skip=true';
       junit '**/target/failsafe-reports/TEST-*.xml'
       archive 'target/*.jar'
    }  
  }
}
