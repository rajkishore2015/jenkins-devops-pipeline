//SCRIPTED

//DECLARATIVE
pipeline {
	agent any
	// agent { docker { image 'maven:3.6.3'} }
	// agent { docker { image 'node:13.8'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
		//def os= System.properties['os.name'].toLowerCase();
	}

	stages {
		stage('Checkout') {
			steps {
				echo "OS: %{os}%"
				//if(os.contains("linux")){
				//sh 'mvn --version'
				//sh 'docker version'
				//echo "Build"
				//echo "PATH - $PATH"
				//echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				//echo "BUILD_ID - $env.BUILD_ID"
				//echo "JOB_NAME - $env.JOB_NAME"
				//echo "BUILD_TAG - $env.BUILD_TAG"
				//echo "BUILD_URL - $env.BUILD_URL"
				//}else{
				bat 'mvn --version'
				bat 'docker version'
					echo "PATH -%PATH%"
				        echo "BUILD_NUMBER - %env.BUILD_NUMBER%"
				        echo "BUILD_ID - %env.BUILD_ID%"
				        echo "JOB_NAME - %env.JOB_NAME%"
				        echo "BUIL_TAG - %env.BUILD_TAG%"
				        echo "BUIL_URL - %env.BUILD_URL%"
				//}
			}
		}
		stage('Compile') {
			steps {
				//if(os.contains("linux")){
				//sh "mvn clean compile"
				//}else{
					bat "mvn clean compile"
				//}
			}
		}

		stage('Test') {
			steps {
				//if(os.contains("linux")){
				//sh "mvn test"
				//}else{
					bat "mvn test"
				//}
			}
		}

		stage('Integration Test') {
			steps {
				//if(os.contains("linux")){
				//sh "mvn failsafe:integration-test failsafe:verify"
				//}else{
					bat "mvn failsafe:integration-test failsafe:verify"
				//}
			}
		}

		stage('Package') {
			steps {
				//if(os.contains("linux")){
				//sh "mvn package -DskipTests"
				//}else{
					bat "mvn package -DskipTests"
				//}
			}
		}

		stage('Build Docker Image') {
			steps {
				//"docker build -t rkishore2019/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("rkishore2019/currency-exchange-devops:${env.BUILD_TAG}")
				}

			}
		}

		stage('Push Docker Image') {
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
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
				//	if(os.contains("linux")){
				//sh "docker run -d --rm -p 8000:8000 --name currency-exchange-devops rkishore2019/currency-exchange-devops:${env.BUILD_TAG}"
    			//echo "Application started on port: 8000 (http)"
			//		}else{
						bat "docker run -d --rm -p 8000:8000 --name currency-exchange-devops rkishore2019/currency-exchange-devops:${env.BUILD_TAG}"
    			echo "Application started on port: 8000 (http)"
			//		}
				}
				 
			}
			
		}
	} 
	
	post {
		always {
			echo 'Im awesome. I run always'
		}
		success {
			echo 'I run when you are successful'
		}
		failure {
			echo 'I run when you fail'
		}
	}
}
