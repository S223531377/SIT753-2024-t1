pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Use Maven to build
                sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests...'
                // Use JUnit for unit tests
                sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Analyzing Code...'
                // Use SonarQube for code analysis
                sh 'mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Performing Security Scan...'
                // Use OWASP Dependency Check for security scanning
                sh 'mvn dependency-check:check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging...'
                // Deploy to AWS EC2 instance
                sh 'scp target/myapp.jar user@staging-server:/path/to/deploy'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging...'
                // Use integration test script on staging
                sh 'ssh user@staging-server /path/to/integration-tests.sh'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production...'
                // Deploy to AWS EC2 instance
                sh 'scp target/myapp.jar user@production-server:/path/to/deploy'
            }
        }
    }
    post {
        always {
            echo 'Pipeline has finished.'
        }
        success {
            mail to: 'developer@example.com',
                 subject: "Pipeline Success: ${currentBuild.fullDisplayName}",
                 body: "Good news! The pipeline succeeded.",
                 attachLog: true
        }
        failure {
            mail to: 'developer@example.com',
                 subject: "Pipeline Failed: ${currentBuild.fullDisplayName}",
                 body: "Bad news! The pipeline failed. Please check the attached logs for more details.",
                 attachLog: true
        }
    }
}
