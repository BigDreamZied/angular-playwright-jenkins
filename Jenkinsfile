pipeline {
    agent {
        label 'docker-node'
    }
    stages {
        stage('Run Playwright in Docker') {
            steps {
                script {
                    docker.image('mcr.microsoft.com/playwright:v1.17.2-focal').inside('-v /dev/shm:/dev/shm') {
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
