pipeline {

    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out Mule application code'
            }
        }

        stage('Build Mule Application') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Mule tests'
            }
        }

        stage('Deploy to CloudHub 2.0') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'anypoint-developer-edition-creds',
                        usernameVariable: 'CLIENT_ID',
                        passwordVariable: 'CLIENT_SECRET'
                    )
                ]) {

                    bat '''
                  mvn clean deploy ^
-DskipExchangeDeploy=true ^
-DclientId=%CLIENT_ID% ^
-DclientSecret=%CLIENT_SECRET%
                    '''

                }
            }
        }

    }
}