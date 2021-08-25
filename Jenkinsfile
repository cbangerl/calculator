pipeline{
	agent any
	stages{
		stage("compile"){
			steps{
				sh "./gradlew compileJava"
				echo "compile successful"
			}
		}
		stage("unittest"){
			steps{
				sh "./gradlew test"
			}
		}


		stage('Sonarqube') {
			environment {
				scannerHome = tool 'SonarQubeScanner'
			}
			steps {
				withSonarQubeEnv('sonarqube') {
					sh "${scannerHome}/bin/sonar-scanner -D sonar.login=admin -D sonar.password=admin -D sonar.host.url=http://localhost:9000/"
				}
				echo "SonarQube check completed"
			}
		}

	}	
}
