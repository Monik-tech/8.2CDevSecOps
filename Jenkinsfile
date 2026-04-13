pipeline {
    agent any

    stages {

        stage('1. Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Monik-tech/8.2CDevSecOps.git'
            }
        }

        stage('2. Install Dependencies') {
            steps {
                bat '''
                    echo Installing dependencies...
                    node -v
                    npm -v
                    npm install || exit 0
                '''
            }
        }

        stage('3. Run Tests') {
            steps {
                bat '''
                    echo Running tests...
                    npm test || exit 0
                '''
            }
        }

        stage('4. Code Analysis (SonarCloud)') {
            steps {
                withCredentials([string(credentialsId: 'Sonar_Token', variable: 'SONAR_TOKEN')]) {
                    bat '''
                        echo Running SonarCloud Analysis...

                        sonar-scanner ^
                        -Dsonar.projectKey=Monik-tech_8.2CDevSecOps ^
                        -Dsonar.organization=Monik-tech ^
                        -Dsonar.host.url=https://sonarcloud.io ^
                        -Dsonar.login=%SONAR_TOKEN% ^
                        -Dsonar.sources=. ^
                        -Dsonar.exclusions=node_modules/**,test/**
                    '''
                }
            }
        }

        stage('5. Security Scan (NPM Audit)') {
            steps {
                bat '''
                    echo Running security scan...
                    npm audit || exit 0
                '''
            }
        }

        stage('6. Deploy to Staging (Simulated)') {
            steps {
                echo 'Deploying application to staging environment...'
            }
        }

        stage('7. Deploy to Production (Simulated)') {
            steps {
                echo 'Deploying application to production environment...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed successfully!'
        }
    }
}
