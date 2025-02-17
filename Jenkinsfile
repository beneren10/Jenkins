pipeline {
    agent any
	environment {
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockeHome/bin:$mavenHome/bin:$PATH"
	}
    stages {
        stage('Checkout') {
            steps {
				sh 'mvn --version'
				sh 'docker --version'
                echo "Build"
                echo "Path: $PATH"
                echo "Build Number: $env.BUILD_NUMBER"
                echo "Build ID: $env.BUILD_ID"
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
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
        stage('Test') {
            steps {
                echo 'Test'
				sh "mvn test"
            }
        }
        stage('Integration Test') {
            steps {
                echo 'Integration Test'
            }
        }
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage("build Docker Image"){
			steps{
				script {
					dockerImage = docker.build("beneren10/currency-exchange-devops:${$env.BUILD_TAG}")
				}
			}
		}
		stage("push Docker Image"){
			steps{
				docker.withRegistry('','dockerhub'){
					dockerImage.push()
					dockerImage.push('latest')
				}
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
