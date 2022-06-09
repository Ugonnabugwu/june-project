pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ugonnabugwu/june-project.git'
            }
        }
        stage('Test with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
         stage('Build with maven') {
            steps {
                sh 'cd SampleWebApp && mvn package'
            }
        }
        stage('Deploy to tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tom-cred', path: '',
                url: 'http://3.14.82.161:8080')], contextPath: 'default', war: '**/*war'
            }
        }
    }
}
