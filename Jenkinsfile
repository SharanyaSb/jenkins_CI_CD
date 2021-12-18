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
		dockerHome = tool 'mydocker'
		mavenHome = tool 'mymaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages{
		stage('Build'){
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER -  $env.BUILD_NUMBER"
				echo "JOB_NAME -  $env.JOB_NAME"
				echo "BUILD_ID -  $env.BUILD_ID"
				echo "BUILD_TAG -  $env.BUILD_TAG"
				echo "BUILD_URL -  $env.BUILD_URL"
			}
		}
		stage('Compile'){
			steps{
				sh "mvn clean compile"
				echo "Test"
			}
		}
		stage('test'){
			steps{
				sh "mvn test"
				echo "Test"
			}
		}
		stage('Integration test'){
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
				echo "Test"
			}
		}

		stage('Package'){
			steps{
				sh "mvn package -DskipTests"
				echo "Test"
			}
		}

		stage('Build docker image'){
			steps{
				//"docker build -t sharanyasb/currency-exchange-devops:$env.BUILD_TAG"
				script{
					dockerImage = docker.build("sharanyasb/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push docker image'){
			steps{
				script{
					docker.withRegistry('', 'dockerhub'){
					dockerImage.push();
					dockerImage.push('latest');
					}
				}
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