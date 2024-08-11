pipeline {
    agent { label 'docker-enabled-node' } // Use a label for a node with Docker installed
    stages {
        stage('Run Playwright in Docker') {
            steps {
                script {
                    docker.image('mcr.microsoft.com/playwright:v1.46.0-jammy').inside('-v /dev/shm:/dev/shm') {
                        sh '''
                            npm install -D @playwright/test
                            npx playwright install
                            npx playwright test --list
                            npx playwright test
                        '''
                    }
                }
            }
        }
    }
}
