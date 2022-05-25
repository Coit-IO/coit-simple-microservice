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
		stage('Checkout'){
			steps{
				checkout([$class: 'GitSCM', branches: [[name: '*/develop']], extensions: [],
				 gitTool: 'Default', userRemoteConfigs: [[url: 'https://github.com/SrashtiD/coit-simple-microservice.git']]]) 
			}	
		}
        stage('Build coit-frontend'){
            steps{
                dir('./coit-frontend'){
				script{
				//def FRONTENDDOCKER = 'Dockerfile-multistage'
				//DockerFrontend = docker.build("srashtid/coitfrontend:${env.BUILD_TAG}","-f ${FRONTENDDOCKER} .")
				sh "docker build -t srashtid/coitfrontend:v1 -f Dockerfile-multistage ."
				
				}
				} 
            }
        }
		stage('Push Frontend to ACR'){
			steps{
				script{
					docker.withRegistry("http://${registryUrl}",registryCredential){
						//DockerFrontend.push();
						//DockerFrontend.push('latest');
						sh "docker push srashtid/coitfrontend:v1"
					}
				}

			}
		}
		stage('Build backend2'){
            steps{
                dir('./coit-backend2'){
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

}
