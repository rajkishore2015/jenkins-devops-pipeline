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
	stages{
		stage('Build') {
			steps{
				// sh "mvn --version"
				echo "Build"
				echo "PATH -$PATH "
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "JOB_NAME - $env.JOB_NAME"
				echo "BUIL_TAG - $env.BUILD_TAG"
				echo "BUIL_URL - $env.BUILD_URL"

			}
			
		}
		stage('Test') {
			steps{
				echo "Test"
			}
			
		}
		stage('IntegrationTest') {
			steps{
				echo "IntTest"
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