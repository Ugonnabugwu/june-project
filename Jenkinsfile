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
    }
}
