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
	stages{
		stage('Build') {
			steps{
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