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
		sh 'chmod 777 /var/lib/jenkins/workspace/2@tmp'
		sh 'rm -rf /var/lib/jenkins/workspace/2/*.war'
		sh 'cp /var/lib/jenkins/workspace/2/java-sample-app/target/*.war /var/lib/jenkins/workspace/2/'
		sh 'cp /var/lib/jenkins/workspace/1/* /var/lib/jenkins/workspace/2/'
	    }
          }
	   stage ('docker') {
            steps {
		sh 'docker build -f Dockerfile.txt -t pp:latest .'
		sh 'docker tag pp praveeenkumarm373/pp:latest'
		sh 'docker push praveeenkumarm373/pp:latest'
	    }
          } 
    }
}
