pipeline {
    agent {
        label 'docker-node'  // Label of a Jenkins node with Docker installed
    }
    stages {
        stage('Install Playwright') {
            steps {
                script {
                    docker.image('mcr.microsoft.com/playwright:v1.46.0-focal').inside('-v /dev/shm:/dev/shm') {
                        sh '''
                            npm install -D @playwright/test
                            npx playwright install
                        '''
                    }
                }
            }
        }
        stage('Help') {
            steps {
                script {
                    docker.image('mcr.microsoft.com/playwright:v1.46.0-focal').inside('-v /dev/shm:/dev/shm') {
                        sh 'npx playwright test --help'
                    }
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    docker.image('mcr.microsoft.com/playwright:v1.46.0-focal').inside('-v /dev/shm:/dev/shm') {
                        sh '''
                            npx playwright test --list
                            npx playwright test
                        '''
                    }
                }
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
