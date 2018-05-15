pipeline {
	agent none
	environment {
		NODE_VER = '8.1.0'
	}

	stages {
		stage('Beginning') { agent any
			environment {
				DEPLOY_VERSION = 'stage'
			}
			steps {
				echo 'Hello world'
				sh 'echo $NODE_VER'
				echo "${env.NEW_VAR}"
			}
		}

		stage('Who Am I?') { agent any
			environment {
				DEPLOY_VERSION = 'prod'
			}
			steps {
				echo "${env.NEW_VAR}"
				sh 'host -t TXT pgp.michaelholley.us |awk -F \'"\' \'{print $2}\''
			}
		}

		stage('Deploy to stage?') {agent none
			steps {
				input 'Deploy to stage?'
			}
		}

		stage('Parallel') {
			failFast true
			parallel {
				stage('Build 1') {agent any
					steps {
						echo "It's ME!"
					}
				}

				stage('Build 2') {agent any
					steps {
						echo "Not it's me!"
					}
				}
			}
		}
	}
}
