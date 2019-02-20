pipeline {
	agent any
    stages {
        stage ('checkout') {
            steps {
		checkout scm
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn -f java-sample-app/pom.xml clean install' 
	    }
          }
    stage ('copy') {
            steps {
                sh 'rm -rf /var/lib/jenkins/workspace/1/*.war'
		sh 'mv /var/lib/jenkins/workspace/2/java-sample-app/target/*.war /var/lib/jenkins/workspace/1/'
	    }
          }
	   stage ('docker') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/1/'
		sh 'docker build -f Dockerfile.txt -t pp:latest .'
		sh 'docker tag pp praveeenkumarm373/pp:latest'
		sh 'docker push praveeenkumarm373/pp:latest'
	    }
          } 
    }
}
