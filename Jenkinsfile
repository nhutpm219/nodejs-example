pipeline {
	agent any

	stages {
	    
	    stage('Check Out') {
			steps {
				git 'https://github.com/nhutpm219/nodejs-example.git'
			}
		}

		stage('Build') {
			steps {
				sh 'docker build -t be4e/nodeapp_test:latest .'
			}
		}

		stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh 'docker push be4e/nodeapp_test:latest'
                }
            }
        }
	}

	post {
		always {
			sh 'docker logout'
		}
	}
}