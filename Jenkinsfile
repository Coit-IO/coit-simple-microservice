pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
triggers {
        cron('H/15 * * * *')
    }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
