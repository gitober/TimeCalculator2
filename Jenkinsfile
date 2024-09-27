pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from your Git repository
                git url: 'https://github.com/gitober/TimeCalculator2.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run Maven build (use bat for Windows)
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests (use bat for Windows)
                bat 'mvn test'
            }
            post {
                always {
                    // Publish JUnit test results
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                // Generate JaCoCo coverage report (use bat for Windows)
                bat 'mvn jacoco:report'
            }
            post {
                always {
                    // Publish JaCoCo coverage report
                    jacoco execPattern: 'target/jacoco.exec', classPattern: 'target/classes', sourcePattern: 'src/main/java', inclusionPattern: '**/*.class'
                }
            }
        }
    }

    post {
        always {
            // Cleanup workspace
            cleanWs()
        }
    }
}