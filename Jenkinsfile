pipeline {
    agent any
    
    environment {
        CODE_DIRECTORY = "/direct/codefolder/access/"
        TESTING_ENV = "testing_my_environment"
        PROD_ENV = "Website_Sajib_Mitra"
    }
    
    stages {
        stage('Building') {
            steps {
                echo "Fetching source code from: ${env.CODE_DIRECTORY}"
                sh 'mvn clean package' // Example Maven build command
            }
        }
        
        stage('Automated Testing') {
            steps {
                echo "Executing automated unit tests"
                sh 'mvn test' // Example Maven test command
                echo "Running integration tests"
            }
        }
        
        stage('Code Analysis and Quality Check') {
            steps {
                echo "Performing code quality analysis"
                // Example command for SonarQube analysis
                sh 'sonar-scanner -Dsonar.projectKey=my_project_key -Dsonar.sources=src'
            }
        }
        
        stage('Deploy to Test') {
            steps {
                echo "Deploying the application to ${env.TESTING_ENV}"
                // Example deployment script
                sh './deploy_to_test.sh'
            }
        }
        
        stage('Manual Approval') {
            steps {
                echo "Waiting for manual approval..."
                input "Please approve deployment to production"
            }
        }
        
        stage('Deploy to Production Env') {
            steps {
                echo "Deploying the code to ${env.PROD_ENV}"
                // Example deployment script
                sh './deploy_to_prod.sh'
            }
        }
    }
    
    post {
        failure {
            mail to: "rathishivang5556@gmail.com",
            subject: "Build Status Email ",
            body: "Build failed. Please check Jenkins for details."
        }
        success {
            mail to: "rathishivang5556@gmail.com",
            subject: "Build Status Email ",
            body: "Build successful. Congratulations!"
        }
    }
}
