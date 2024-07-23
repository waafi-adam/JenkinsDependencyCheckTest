pipeline {
    agent any
    environment {
        NVD_API_KEY = credentials('nvd-api-key-id') // Replace with your Jenkins credential ID
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/waafi-adam/JenkinsDependencyCheckTest', branch: 'master'
            }
        }
        stage('OWASP DependencyCheck') {
            steps {
                dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey $NVD_API_KEY', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
