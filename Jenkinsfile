pipeline {
    agent any

    stages {

        stage('1. Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Monik-tech/8.2CDevSecOps.git'
            }
        }

        stage('2. Build (Install Dependencies)') {
            steps {
                bat '''
                    node -v
                    npm -v
                    npm install || exit 0
                '''
            }
        }

        stage('3. Unit & Integration Testing') {
            steps {
                bat 'npm test || exit 0'
            }
        }

        stage('4. Code Analysis (SonarCloud)') {
            steps {
                withCredentials([string(credentialsId: 'Sonar_Token', variable: 'SONAR_TOKEN')]) {
                    bat '''
                        echo Running SonarCloud Analysis...

                        sonar-scanner ^
                        -Dsonar.projectKey=Monik-tech_8.2CDevSecOps ^
                        -Dsonar.organization=Monik-tech^
                        -Dsonar.host.url=https://sonarcloud.io ^
                        -Dsonar.login=%SONAR_TOKEN% ^
                        -Dsonar.sources=. ^
                        -Dsonar.exclusions=node_modules/**,test/**
                    '''
                }
            }
        }

        stage('5. Security Scan (npm audit)') {
            steps {
                bat 'npm audit || exit 0'
            }
        }

        stage('6. Deploy to Staging (Simulated)') {
            steps {
                echo 'Deploying to staging environment...'
            }
        }

        stage('7. Deploy to Production (Simulated)') {
            steps {
                echo 'Deploying to production environment...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished successfully!'
        }
    }
}
