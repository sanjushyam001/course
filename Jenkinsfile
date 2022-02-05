pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "m3"
    }

    stages {
        stage('git clone') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/vasishta-github/course.git'
            }
        }
        stage ('building the package') {
            steps{
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage ('deploy to tomcat') {
            steps{
                // deploy to tomcat
                deploy adapters: [tomcat9(credentialsId: 'tomcat_credentials', path: '', url: 'http://65.2.152.44:8080//')], contextPath: '/course', war: '**/*.war'
            }
        }
        
    }
}
