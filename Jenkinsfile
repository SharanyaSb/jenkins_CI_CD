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
	//agent { docker { image 'maven:3.6.3'}}

	environment{
		dockerHome = tool'mydocker'
		mavenHome = tool'mymaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build'){
			steps{
				sh 'mvn --version'
				echo "Test"
			}
		}
		stage('Integrationtest'){
			steps{
				echo "mvn clean complie"
				echo "Test"
			}
		}
		stage('test'){
			steps{
				echo "mvn test"
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