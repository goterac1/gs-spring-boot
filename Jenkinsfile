pipeline {
	agent any

	tools {
		maven 'maven-3.9.11'
	}

	environment {
		NEXUS_URL = 'http://localhost:8081/repository/maven-releases'

		GROUP_PATH = 'org/springframework/gs'
		ARTIFACT_ID = 'gs-spring-boot'
		VERSION = '0.1.0'

		PACKAGING = 'jar'
		FILE = "target/${ARTIFACT_ID}-${VERSION}.jar"

		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin'
	}

	stages { 
		stage('Checkout') {
			steps {
				checkout scm
			}
		}

		stage("Build Spring Boot Jar') {
			steps {
				sh 'mvn -B clean package'
			}
		}

		stage('Upload to Nexus') {
			steps {
				sh """
				curl -v -u $NEXUS_USER:$NEXUS_PASS \
					--upload-file $FILE \
					$NEXUS_URL/$GROUP_PATH/$ARTIFACT_ID/$VERSION/$ARTIFACT_ID-$VERSION.$PACKAGING
					"""
				}
			}
		}
	}
}

