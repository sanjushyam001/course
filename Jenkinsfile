pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3"
    }

    stages {
        stage('Cloning from GitHub') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/vasishta-github/course.git'
            }
        }
        stage('Building the artifact') {
            steps {
                
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Deploying artifact') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat_credentials', path: '', url: 'http://3.111.213.92:8899/')], contextPath: '/course', war: '**/*.war'
            }
        }
		}
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    archiveArtifacts 'target/*.war'
            }
        
        }
}
