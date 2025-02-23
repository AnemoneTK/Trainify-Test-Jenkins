// pipeline {
//     agent any
//     stages {
//         stage('Clone') {
//             steps {
//                 script {
//                     print "Cloning repository..."
//                     checkout([
//                         $class: 'GitSCM',
//                         branches: [[name: '*/main']],
//                         userRemoteConfigs: [[
//                             credentialsId: '76fb8aa3-686a-47ae-863a-772e8e12c160',
//                             url: 'https://github.com/AnemoneTK/Trainify-Test-Jenkins.git'
//                         ]]
//                     ])
//                     print "Repository cloned successfully."
//                 }
//             }
//         }

//         stage('verify tooling') {
//             steps {
//                 sh '''
//                     docker version
//                     docker info
//                     docker compose version
//                     curl --version
//                     jq --version
//                 '''
//             }
//         }
//         stage('Prune Docker data') {
//             steps {
//                 sh 'docker system prune -a --volumes -f'
                    
//             }
//         }
//         stage('Start container') {
//             steps {
//                 script {
//                     print "Building Docker images..."
//                     // ใช้ docker-compose เพื่อ build Docker image
//                     sh 'docker-compose up -d'
//                     sh 'docker compose ps'
//                     print "Docker image build completed."
//                 }
//             }
//         }
//     }

//     post {
//         always {
//             echo 'Pipeline execution finished.'
//         }
//         success {
//             echo 'Build and deployment successful.'
//         }
//         failure {
//             echo 'Build or deployment failed.'
//         }
//     }
// }
pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                script {
                    print "Cloning repository..."
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: '76fb8aa3-686a-47ae-863a-772e8e12c160',
                            url: 'https://github.com/AnemoneTK/Trainify-Test-Jenkins.git'
                        ]]
                    ])
                    print "Repository cloned successfully."
                }
            }
        }

        stage('Verify Docker') {
            steps {
                script {
                    print "Verifying Docker installation..."
                    sh 'docker --version'
                    print "Docker is installed successfully."
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    print "Building Docker images..."
                    sh 'docker-compose -f docker-compose.yml build'
                    print "Docker image build completed."
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    print "Deploying Docker containers..."
                    sh 'docker-compose -f docker-compose.yml up -d'
                    print "Docker containers are running."
                }
            }
        }
    }
}
