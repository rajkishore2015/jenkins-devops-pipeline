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
	// agent any
	agent{docker{image 'maven:3.6.3'}}
	stages{
		stage('Build') {
			steps{
				sh "mvn --version"
				echo "Build"
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