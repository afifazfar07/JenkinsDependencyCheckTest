pipeline {
	agent any
	stages {
		stage('Checkout SCM') {
			steps {
				echo 'Git Checkout'
			}
		}

		stage('Check OWASP') {
           steps {
                echo 'Check OWASP Stage'
                // Add your OWASP Dependency-Check configuration here if needed
                dependencyCheck additionalArguments: ''' 
                     -o './'
                     -s './'
                     -f 'ALL' 
                     --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml' 
            }
        }
	}	
	post {
		success {
			dependencyCheckPublisher pattern: 'dependency-check-report.xml'
		}
	}
}