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
	  stage('Code Quality Check via SonarQube') {

   		steps {

       script {

       def scannerHome = tool 'Sonar';

           withSonarQubeEnv("sonarqube-scan") {

           sh "${tool("sonarqube")}/bin/sonar-scanner 

           -Dsonar.projectKey=new_test

           -Dsonar.sources=. 

           -Dsonar.host.url=http://localhost:9000 

           -Dsonar.login=sqp_81758515d369729c5a365fc5bd79dcdfe3f31e82

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
