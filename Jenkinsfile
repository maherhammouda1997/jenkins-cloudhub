def config ={}
def env = {}
pipeline {
    agent any
    stages {
		stage('Setup Configuration') {
            steps {
				script {
					config = readJSON (file: "env/${env.BRANCH_NAME}/config.json")
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
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				sh "mvn -Dmaven.test.failure.ignore=true clean deploy -DmuleDeploy -Dworkers=1 -Dworker.type=Micro -DapplicationName=${env.applicationName} -DmuleVersion=${env.muleVersion} -Denvironment=${environment}"          
            }
        }
    }
}
