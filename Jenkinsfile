pipeline {
  agent any

  stages {
    stage('Build & Unit test') {
      steps {
        sh 'mvn clean package'
      }
    }

  stage('Static Code Analysis'){
       environment{
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps{
                withSonarQubeEnv('SONAR_LOCAL'){
                    sh '${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployFront -Dsonar.host.url=http://localhost:9000 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java'
                }
            }
    }
  post{
        always{
            junit allowEmptyResults: true, testResults:'target/surefire-reports/*.xml'
        }
      }
  }
}
