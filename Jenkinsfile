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
			steps{
				dependencyCheck additionalArguments: '''
                   -o './'
                   -s './'
                   -f 'ALL'
				   --noupdate
                   --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
       			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
			}
		}
	}
}