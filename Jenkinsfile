def config ={}
def env = {}
pipeline {
    agent any
    stages {
		stage('Setup Configuration') {
            steps {
				echo "Setup Configuration"
				script {
					config = readJSON file: "env/${env.BRANCH_NAME}/config.json"
					env = config.get("envConfig")
				}
			}
		}
		
        stage('Build') {
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
		
		stage('Test') {
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				sh "mvn -Dmaven.test.failure.ignore=true clean test"
            }
        }
        
        stage('Deploy') {
			environment {
				'ANYPOINT_CREDENTIALS_USR' = credentials ('e66340e2-d15e-4fa4-96a2-70db4e8dda1e').username
				'ANYPOINT_CREDENTIALS_PSW' = credentials ('e66340e2-d15e-4fa4-96a2-70db4e8dda1e').password
			}
            steps {			   
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				sh "mvn -Dmaven.test.failure.ignore=true clean deploy -DmuleDeploy -Dworkers=1 -Dworker.type=Micro" + 
				"-DapplicationName=${env.applicationName} -DmuleVersion=${env.muleVersion} -Denvironment=${env.environment}" +
				"-Danypoint.username=${env.ANYPOINT_CREDENTIALS_USR} -Danypoint.password=${env.ANYPOINT_CREDENTIALS_PSW}" 
 				
            }
        }
    }
}
