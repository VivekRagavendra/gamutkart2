pipeline {
    agent any

//	tools {
//		maven 'maven3.6'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    steps {
	        checkout scm
	    }
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "vivek" scp target/gamutgurus.war vivek@172.17.0.3:/home/vivek/apache-tomcat-9.0.65/webapps'
                sh 'sshpass -p "vivek" ssh vivek@172.17.0.3 "/home/vivek/apache-tomcat-9.0.65/bin/startup.sh"'
            }
        }
    }
}
