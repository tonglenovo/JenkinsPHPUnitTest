pipeline {
	agent{
		docker {
			image 'composer:latest'
		}
	}
	stages {
		stage('Build') {
			steps {
				sh 'composer install'
			}
		}
		stage('Check JAVA_HOME') {
            steps {
                script {
                    echo "JAVA_HOME is set to ${env.JAVA_HOME}"
                    sh 'echo $JAVA_HOME'
                    sh 'java -version'
                }
            }
        }
		stage('Test') {
			steps {
                sh './vendor/bin/phpunit tests'
            }
		}
		stage('OWASP') {
			steps {
				dependencyCheck additionalArguments: '--format HTML --format XML --noupdate', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
			}
		}
	}
}