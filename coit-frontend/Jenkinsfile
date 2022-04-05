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
            emailext body: '''Jenkins has failed to build the Job. Please find the information below.

                            Name of the Job: ${JOB_NAME}
                            Build that failed: ${BUILD_NUMBER}

                            Please check the logs at ${BUILD_URL}


                            Thanks
                            Jenkins''', subject: 'Failed ${JOB_NAME}', to: 'basil@coit.io'
        }
    }
}