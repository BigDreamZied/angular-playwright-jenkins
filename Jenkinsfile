pipeline {
    agent { 
        docker { 
            image 'mcr.microsoft.com/playwright:v1.46.0-focal'
            args '-v /dev/shm:/dev/shm'  
        } 
    }
    stages {
        stage('Install Playwright') {
            steps {
                sh '''
                    npm install -D @playwright/test
                    npx playwright install
                '''
            }
        }
        stage('Help') {
            steps {
                sh 'npx playwright test --help'
            }
        }
        stage('Run Tests') {
            steps {
                sh '''
                    npx playwright test --list
                    npx playwright test
                '''
            }
            post {
                success {
                    archiveArtifacts artifacts: 'homepage-*.png', followSymlinks: false
                }
                cleanup {
                    sh 'rm -rf homepage-*.png'
                }
            }
        }
    }
}
