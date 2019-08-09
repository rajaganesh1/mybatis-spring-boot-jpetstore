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
		stage('Test') {
            steps {
                sh 'mvn test'
            }
			
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    step([$class: 'CoberturaPublisher', autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/coverage.xml', failUnhealthy: false, failUnstable: false, maxNumberOfBuilds: 0, onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false])

                }
            }
			}
		stage('Cobertura - report') {
            steps {
                sh 'mvn cobertura:cobertura'
            }
        }
           
    }
}
