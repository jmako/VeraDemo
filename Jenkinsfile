pipeline {
    agent any
	
	environment {
	    JAVA_HOME = 'C:/Program Files/Java/jdk1.8.0_101'
	}


	stages {
        stage('---clean---') {
            steps {
                bat "mvn clean"
            }
        }
        stage('---test---') {
            steps {
                bat "mvn test"
            }
        }
        stage('---package---') {
            steps {
                bat "mvn package"
            }
        }
		stage('---Veracode Scan---') {
            steps {
			    withCredentials([usernamePassword(credentialsId: '30925d33-3b62-4d2c-85ae-45de4e9df498', usernameVariable: 'VERACODE_API_ID', passwordVariable: 'VERACODE_API_KEY')]) {
                    veracode applicationName: 'VeraDemo', criticality: 'Medium', debug: true, fileNamePattern: '', replacementPattern: '', sandboxName: '', scanExcludesPattern: '', scanIncludesPattern: '', scanName: '$buildnumber', teams: '',timeout: 30, uploadExcludesPattern: '', uploadIncludesPattern: '**/**.war', useIDkey: true, vid: "${VERACODE_API_ID}", vkey: "${VERACODE_API_KEY}"
                		}
			}
		}
         stage('---deploy---') {
            steps {
                echo 'Deploying....'
            }
         }
    
    }
}