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