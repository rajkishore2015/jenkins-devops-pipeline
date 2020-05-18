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
	}
	stages{
		stage('Checkout') {
			steps{
				sh "mvn --version"
				sh "docker --version"
				echo "Build"
				echo "PATH -$PATH "
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUIL_TAG - $env.BUILD_TAG"
				echo "BUIL_URL - $env.BUILD_URL"

			}
			
		}
		stage('Compile') {
			steps{
				sh "mvn clean install compile"
			}
		}
		stage('Test') {
			steps{
				sh "mvn test"
			}
		}
		stage('IntegrationTest') {
			steps{
				echo "mvn failsafe:integration-test failsafe:verify"
			}
			
		}
		stage('Package') {
			steps{
				echo "mvn clean package -DskipTests"
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
						dockerImage.push('latest');

					}

				}
				 sh "docker run -d --rm -p $httpPort:$httpPort --name $containerName $dockerHubUser/$containerName:$tag"
    			echo "Application started on port: ${httpPort} (http)"
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