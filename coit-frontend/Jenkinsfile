pipeline{
    agent any
    stages{
        stage("Build"){
            steps{
                sh 'cd coit-frontend && npm install && npm run build'
            }
        }
        stage("Setup Env"){
            steps{
                sh "echo Installing Apache"
            }
        }
        stage("Deploy"){
            steps{
                sh "echo Deploying the build folder"
            }
        }
        stage("Cleanup"){
            steps{
                deleteDir()
            }
        }
    }
    post{
        success{
            archiveArtifacts artifacts: '**/build', followSymlinks: false
        }
        failure{
            emailext body: 'Build has failed. Please check.', subject: 'Build Failed ', to: 'basil@coit.io'
        }
    }
}