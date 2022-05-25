pipeline{
    agent any
    environment{
		registryName = "coitACR"
		registryUrl = "coitACR.azurecr.io"
		registryCredential = "ACR"
		mavenHome = tool 'mymaven'
		dockerHome = tool 'mydocker'
		gitHome = tool 'myGit'
		PATH = "$dockerHome/bin:$mavenHome/bin:$gitHome/bin:$PATH"
	}
	stages{
		stage('Build Information'){
			steps{
				sh 'mvn --version'
				sh 'docker --version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "JOB_NAME - $env.JOB_NAME"
				//checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [],
				// gitTool: 'Default', userRemoteConfigs: [[url: 'https://github.com/SrashtiD/Coit-Jenkins']]]) 
			}	
		}
        stage('Build '){
            steps{
                dir('./coit-frontend'){
				echo "path- $PATH"
				script{
				def FRONTENDDOCKER = 'Dockerfile-multistage'
				DockerFrontend = docker.build("srashtid/coitfrontend:${env.BUILD_TAG}","-f ${FRONTENDDOCKER} .")
				//sh('docker build -t srashtid/coitfrontend:v1 -f Dockerfile-multistage . > DockerFrontend')
				
				}
				} 
            }
        }
		stage('Push Frontend to ACR'){
			steps{
				script{
					docker.withRegistry("http://${registryUrl}",registryCredential){
						DockerFrontend.push();
						//DockerFrontend.push('latest');
					}
				}

			}
		}
		stage('Build backend2'){
            steps{
                dir('./coit-backend2'){
				echo "path- $PATH"
				script{
				DockerBackend2 = docker.build("srashtid/coitbackend2:${env.BUILD_TAG}")
				//DockerBackend2 = sh('docker build -t srashtid/coitbackend2:v1 -f ./coit-backend2/Dockerfile .')
				}
				}
                
            }
        }
		stage('Push backend2'){
			steps{
				script{
					//docker.withRegistry('','dockerhub'){
					docker.withRegistry("http://${registryUrl}",registryCredential){
						DockerBackend2.push();
						//DockerBackend2.push('latest');
					}
				}

			}
		}
		stage('Build backend1'){
            steps{
                dir('./coit-backend1'){
					script{
					def BACKENDDCKER = 'Dockerfile-multistage'
					DockerBackend1 = docker.build("srashtid/coitbackend1:${env.BUILD_TAG}","-f ${BACKENDDCKER} .")
					//DockerBackend1 = sh('docker build -t srashtid/coitbackend2:v1 -f ./coit-backend2/Dockerfile .')
					}
				}
                
            }
        }
		stage('Push backend1'){
			steps{
				script{
					docker.withRegistry("http://${registryUrl}",registryCredential){
						DockerBackend1.push();
						//DockerBackend1.push('latest');
					}
				}

			}
		}
		
    }
	post {
			always{
				echo "Im awesome. I run always"
			}
			success{
				echo 'I run when you are successful'
			}
			failure{
				echo 'I run when you fail'
			}
		}
	

}
