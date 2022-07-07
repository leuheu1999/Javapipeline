pipeline {
    agent any

    stages {
        stage ('Compile Stage') {

            steps {
                withMaven(maven : 'M3') {
                    bat 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage') {

            steps {
                withMaven(maven : 'M3') {
                    bat 'mvn test'
                }
            }
        }

    stage('SonarQube analysis') {
      steps {
        script {
          def scannerHome = tool 'Sonar';
          withSonarQubeEnv('sonarqube') {
            sh "${tool("sonarscan ")}/bin/sonar-scanner -Dsonar.projectKey=new_test -Dsonar.projectName=new test"
          }
        }
      }
    }
    stage("Quality gate") {
      steps {
        script {
          def qualitygate = waitForQualityGate()
          sleep(10)
          if (qualitygate.status != "OK") {
            waitForQualityGate abortPipeline: true
          }
        }
      }
    }
  }
}

        stage ('Deployment Stage') {
            steps {
                withMaven(maven : 'M3') {
                    bat 'mvn deploy'
                }
            }
        }
    }
}
           
