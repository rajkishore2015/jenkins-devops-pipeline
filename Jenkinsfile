// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('IntegrationTest') {
// 		echo "IntTest"
// 	}
// }
// node {
// 		echo "Build"
// 		echo "Test"
// 		echo "IntTest"
	
// }


pipeline{
	agent any
	// agent{docker{image 'maven:3.6.3'}}
	environment{
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		dockerImage = ''
		PATH= "$dockerHome/bin:$mavenHome/bin:$PATH:"
		def os= System.properties['os.name'].toLowerCase();
		
		//echo "PATH -$PATH "
	}
	stages{
		stage('Checkout') {
			steps{
				echo "OS: %{os}%"
                	if(os.contains("linux")){
					sh "mvn --version"
				    sh "docker --version"
				    echo "Build"
				    echo "PATH -$PATH "
				    echo "PATH -%PATH%"
				    echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				    echo "BUILD_ID - $env.BUILD_ID"
				    echo "JOB_NAME - $env.JOB_NAME"
				    echo "BUIL_TAG - $env.BUILD_TAG"
				    echo "BUIL_URL - $env.BUILD_URL"
	       		}else{
                        bat "mvn --version"
			        	bat "docker --version"						       
				        echo "PATH -%PATH%"
				        echo "BUILD_NUMBER - %env.BUILD_NUMBER%"
				        echo "BUILD_ID - %env.BUILD_ID%"
				        echo "JOB_NAME - %env.JOB_NAME%"
				        echo "BUIL_TAG - %env.BUILD_TAG%"
				        echo "BUIL_URL - %env.BUILD_URL%"
			 }
			}
			
		}
		stage('Compile') {
			steps{
				    if(os.contains("linux")){
					    sh "mvn clean install compile"
			    	}
				    else{
					        bat "mvn clean install compile"						       
			    	}		       
			}
		}
		stage('Test') {
			steps{
				    if(os.contains("linux"))
                    {
					    sh "mvn test"
				    }
				    else{
					    bat "mvn test"
				    }	
				
			}
		}
		stage('IntegrationTest') {
			steps{
				    echo "mvn failsafe:integration-test failsafe:verify"
				if(os.contains("linux")){
					sh "mvn failsafe:integration-test failsafe:verify"
				}
				else{
					bat "mvn failsafe:integration-test failsafe:verify"
				}
			}
			
		}
		stage('Package') {
			steps{
				echo "mvn clean package -DskipTests"
				
				    if(os.contains("linux"))
                    {
					    sh "mvn clean package -DskipTests"
				    }
				    else{
					    bat "mvn clean package -DskipTests"
				    }
			}
			
		}
		stage('Build Docker Image') {
			steps{
				// docker build  -t rkishore2019/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("rkishore2019/currency-exchange-devops:${env.BUILD_TAG}")
					
				}
			}
			
		}
		stage('Push Docker Image') {
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
			
		}
		stage('Run Docker Image') {
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.pull();
						
					}
				sh "docker run -d --rm -p 8000:8000 --name currency-exchange-devops rkishore2019/currency-exchange-devops:${env.BUILD_TAG}"
    			echo "Application started on port: 8000 (http)"
				}
				 
			}
			
		}
	}
	post{
		always{
			echo "Im always awesome. I run always"
		}
		success{
			echo " I run always when success"
		}
		failure{
			echo " I run always when failure"
		}
		changed{
			echo " I run always when changed"
		}
	}
}

	}
	stages{
		stage('Checkout') {
			steps{
				echo "OS: %{os}%"
					if(os.contains("linux)){
					sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "PATH -$PATH "
				echo "PATH -%PATH%"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUIL_TAG - $env.BUILD_TAG"
				echo "BUIL_URL - $env.BUILD_URL"
	       
				}
				else{
                                bat "mvn --version"
				bat "docker --version"						       
				echo "PATH -%PATH%"
				echo "BUILD_NUMBER - %env.BUILD_NUMBER%"
				echo "BUILD_ID - %env.BUILD_ID%"
				echo "JOB_NAME - %env.JOB_NAME%"
				echo "BUIL_TAG - %env.BUILD_TAG%"
				echo "BUIL_URL - %env.BUILD_URL%"
				}
			}
			
		}
		stage('Compile') {
			steps{
				if(os.contains("linux)){
					sh "mvn clean install compile"
				}
				else{
					bat "mvn clean install compile"						       
				}		       
			}
		}
		stage('Test') {
			steps{
				if(os.contains("linux)){
					sh "mvn test"
				}
				else{
					bat "mvn test"
				}	
				
			}
		}
		stage('IntegrationTest') {
			steps{
				echo "mvn failsafe:integration-test failsafe:verify"
				if(os.contains("linux)){
					sh "mvn failsafe:integration-test failsafe:verify"
				}
				else{
					bat "mvn failsafe:integration-test failsafe:verify"
				}
			}
			
		}
		stage('Package') {
			steps{
				echo "mvn clean package -DskipTests"
				
				if(os.contains("linux)){
					sh "mvn clean package -DskipTests"
				}
				else{
					bat "mvn clean package -DskipTests"
				}
			}
			
		}
		stage('Build Docker Image') {
			steps{
				// docker build  -t rkishore2019/currency-exchange-devops:$env.BUILD_TAG
				script{
					dockerImage = docker.build("rkishore2019/currency-exchange-devops:${env.BUILD_TAG}")
					
				}
			}
			
		}
		stage('Push Docker Image') {
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.push();
						dockerImage.push('latest');
					}
				}
			}
			
		}
		stage('Run Docker Image') {
			steps{
				script{
					docker.withRegistry('','dockerhub'){
						dockerImage.pull();
						
					}
				sh "docker run -d --rm -p 8000:8000 --name currency-exchange-devops rkishore2019/currency-exchange-devops:${env.BUILD_TAG}"
    			echo "Application started on port: 8000 (http)"
				}
				 
			}
			
		}
	}
	post{
		always{
			echo "Im always awesome. I run always"
		}
		success{
			echo " I run always when success"
		}
		failure{
			echo " I run always when failure"
		}
		changed{
			echo " I run always when changed"
		}
	}
}
