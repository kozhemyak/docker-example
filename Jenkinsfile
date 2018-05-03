pipeline {
    agent any
    stages {
        stage('Echo Stage') {
            steps {
                echo "${params.Greeting} World!"
            }
        }

        stage('Make File') {
            steps {
                sh 'pwd'
            }
        }

        stage('[Sleep Stage]') {
            steps {
                sleep 30
            }
        }
    }
}