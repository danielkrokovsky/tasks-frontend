pipeline {
  agent any
  stages{
      stage('Build Backend'){
          steps{
              sh 'mvn clean package -DskipTests=true'
          }
      }
      stage('Unit Tests'){
          steps{
              sh 'mvn test'
          }
      }
      stage('Sonar Analisys'){
          environment{
              scannerHome = tool 'SONAR_SCANNER'
          }
          steps{
              withSonarQubeEnv('SONAR_LOCAL'){
                  sh '${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=1f605deeac7fc695c32c90a080f85492b9719bce -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java'
              }
          }
      }
      stage('Deploy Frontend'){
          steps{
              deploy adapters: [tomcat8(credentialsId: 'f86a9675-12cf-4f09-acbe-03db3086c4e3', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks.war'
          }
      }
  }
      post{
          always{
              junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
        }
  }
}
