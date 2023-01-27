pipeline {
    agent any

    environment {
		DOCKERHUB_CREDENTIALS=credentials('dockerhub')
	}

    stages {

        stage ('Build Docker Image'){
            steps{
                script {
                    dockerapp = docker.build("diogofiaminghi/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }

        stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				//sh 'docker push diogofiaminghi/kube-news:latest'
                //dockerapp.push('latest')
                dockerapp.push("${env.BUILD_ID}")
			}
		}
	}

    post {
        always {
            sh 'docker logout'
        }
    }    
}    

//        stage('Push Docker Image'){
//          steps {
//              script {
//                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
//                        dockerapp.push('latest')
//                        dockerapp.push("${env.BUILD_ID}")
//                }
//           } 
//        }
//    }
