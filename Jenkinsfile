pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('Results') {
      steps {
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('') {
      steps {
        archiveArtifacts 'target/*.jar'
      }
    }

  }
}