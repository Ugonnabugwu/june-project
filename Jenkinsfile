pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/ugonnabugwu/june-project.git'
            }
        }
        
        stage('Test') {
            steps {
                sh 'cd SampleWebApp && mvn test'
            }
        }
        stage('Build with Maven') {
            steps {
                sh 'cd SampleWebApp && mvn clean package'
            }
        }

        stage('Deploy to Staging') {
            when {
               branch "staging"
                }
            steps {
                step([$class: 'AWSEBDeploymentBuilder', credentialId: 'aws-cred',
                awsRegion: 'us-east-2', applicationName: 'june-app', environmentName: 'Juneapp-env1', keyPrefix: 'stage', sleepTime: 5,
                bucketName: 'elasticbeanstalk-us-east-2-697102533223', rootObject: 'SampleWebApp/default/SampleWebApp-1.0.null.war', versionLabelFormat: 'Juneapp-env1-$BUILD_NUMBER'])
                
            }
        }

        stage('Deploy to Prod') {
             when {
               branch "main"
                }
            steps {
                step([$class: 'AWSEBDeploymentBuilder', credentialId: 'aws-cred',
                awsRegion: 'us-east-2', applicationName: 'june-app', environmentName: 'Juneapp-env2', keyPrefix: 'prod', sleepTime: 5,
                bucketName: 'elasticbeanstalk-us-east-2-697102533223', rootObject: 'SampleWebApp/default/SampleWebApp-1.0.null.war', versionLabelFormat: 'Juneapp-env2-$BUILD_NUMBER'])
                
            }
        }
    }
}
