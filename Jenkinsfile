def config ={}
def env = {}
pipeline {
    agent any
	environment {
        ANYPOINT_USERNAME = credentials('mahran_hammouda_')
        ANYPOINT_PASSWORD = credentials('79911997mM.')
    }
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
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				sh "mvn -Dmaven.test.failure.ignore=true clean deploy -DmuleDeploy -Dworkers=1 -Dworker.type=Micro \ 
				-DapplicationName=${env.applicationName} -DmuleVersion=${env.muleVersion} -Denvironment=${env.environment} \
				-Dusername=${ANYPOINT_USERNAME} -Dpassword=${ANYPOINT_PASSWORD}"      
            }
        }
    }
}
