pipeline {
	agent any
	tools {
		maven 'maven 3.9.9'
		jdk 'Java JDK 17'
	}
	stages {
		stage("clean") {
			steps {
				echo "Start Clean"
				bat "mvn clean"
			}
		}
		stage("test") {
			steps {
				echo "Start Test"
				bat "mvn test"
			}
			
		}
		stage("build") {
			steps {
				echo "Start Build"
				bat "mvn install -DskipTests"
			}
		}
        stage('Deploy to Tomcat') {
			steps {
				script {
					// Find the WAR file
            		//def warFile = findFiles(glob: 'target/*.war')[0]
            		def warFile = 'target\\todoApp.war'
            		//echo "Deploying WAR file: ${warFile.path}"
 
					// Tomcat Manager URL and credentials
					def tomcatUrl = 'http://localhost:8090/manager/text'
					def tomcatUser = 'tomcat'
					def tomcatPassword = 'password'
 
					// Deploy the WAR file using curl
					bat """
					curl -v -u ${tomcatUser}:${tomcatPassword} \
					-T ${warFile} \
					${tomcatUrl}/deploy?path=/todoapp
					"""
				}
			}
		}
	}
}