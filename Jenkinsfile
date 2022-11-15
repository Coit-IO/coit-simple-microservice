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

stage('sign the container image') {
            steps {
                sh 'cosign version'
                sh 'cosign sign --key cosign.key 9676164428/coit-frontend:v1'
      }
    }
    }
}
