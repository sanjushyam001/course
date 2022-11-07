pipeline {
    agent any
	
	tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3"
    }

    stages {
        stage('git clone the repo') {
            steps {
                git 'https://github.com/vasishta-github/course.git'
            }
        }
		stage('build the package') {
            steps {
                  sh 'mvn clean package'
			}
        }		
		stage('deploy the artifact') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials', path: '', url: 'http://3.73.129.226:8080/')], contextPath: '/course', war: '**/*.war'
            }
        }
    }
}