pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				bat "mvn -Dmaven.test.failure.ignore=true clean package"
                //sh 'mvn clean install'
            }
        }
		
		stage('Test') {
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				bat "mvn -Dmaven.test.failure.ignore=true clean test"
            }
        }
        
        stage('Deploy') {
            steps {
				git 'https://github.com/maherhammouda1997/jenkins-cloudhub.git'
				bat "mvn -Dmaven.test.failure.ignore=true clean deploy -DmuleDeploy"
                //sh 'mvn package deploy -DmuleDeploy'
            }
        }
    }
}
