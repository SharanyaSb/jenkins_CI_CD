// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('Integration Test') {
// 		echo "Test"
// 	}
// }

// node{
// 	echo "Build"
// 	echo "Test"
// 	echo "Integration Test"
// }

pipeline{
	agent any
	stages{
		stage('Build'){
			steps{
				echo "Build"
				echo "Test"
			}
		}
		stage('Integrationtest'){
			steps{
				echo "integration test"
				echo "Test"
			}
		}
		stage('test'){
			steps{
				echo "test"
				echo "Test"
			}
		}
	}

	post{
		always{
			echo "I always run"
		}
		success{
			echo "I success"
		}
		failure{
			echo "failed"
		}
		changed{
			echo "build subversion changed to pass from fail or fail to pass"
		}
	}

}