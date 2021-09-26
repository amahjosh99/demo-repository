pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/amahjosh99/demo-repository.git']]])
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: '8bda1016-2af4-4a96-a1dd-0c90182e59a8', path: '', 
                url: 'http://18.216.234.236:8080/')], 
                contextPath: 'webapp', war: '**/*.war'
            }
        }
    }
}

