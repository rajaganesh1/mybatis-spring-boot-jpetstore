pipeline {
    agent {label 'docker-maven'}
    stages {
		stage('SCM Checkout') {
		    steps{
			    checkout scm
		      }		
		}
		stage('Build') {
		    steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
		stage('Unit Test & Code Coverage') {
            steps {
                
		    sh 'mvn test cobertura:cobertura'
            }
			
           }
		    
    }
}
