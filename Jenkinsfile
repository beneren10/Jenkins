pipeline {
	// agent {
	// 	docker {
	// 		image 'node:21.7'
	// 	}
	// }
		stages {
			stage('Build') {
				steps {
					echo 'Build'
					echo "Path: $PATH"
					echo "Build Number: $env.BUILD_NUMBER"
					echo "Build ID: $Env.BUILD_ID"
					echo "Build Tag: $env.BUILD_TAG"
					echo "Build URL: $env.BUILD_URL"
					echo "Job Name: $env.JOB_NAME"
				}
				post {
					always {
						echo 'I run at the end of the build stage'
					}
				}
		}
		stage('Test') {
			steps {
				echo 'Test'
			}
		}
		stage('Integration Test') {
			steps {
				echo 'Integration Test'
			}
		}
	}
	post {
		always {
			echo 'I always run'
		}
		success {
			echo 'I run when successful'
		}
		failure {
			echo 'I run when failed'
		}
	}
}