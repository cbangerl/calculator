pipeline{
	agent any
	triggers {
		pollSCM('* * * * *')
	}
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

/*
CNB: SONARQUBE DOES NOT WORK  
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
*/
		stage("package"){
			steps{
				sh "./gradlew build"
			}
		
		}

		stage("Docker build"){
			steps{
				sh "sudo docker build -t calculator ."
				sh "sudo docker tag calculator chrisbanner87/calculator:1"
			}
		}
		
		stage("Docker push"){
			steps{
				sh "sudo docker login --username chrisbanner87 --password 9uxupEB6EYCLK9rR0tZe"
				sh "sudo docker push chrisbanner87/calculator:1"
			}
		}

	}	
}
