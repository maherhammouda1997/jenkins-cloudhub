pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                
                bat 'mvn clean install'
            }
        }
        
        stage('Deploy') {
            steps {
                bat 'mvn package deploy -DmuleDeploy'
            }
        }
    }
}