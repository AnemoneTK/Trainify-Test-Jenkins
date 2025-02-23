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

        stage('Build') {
            steps {
                script {
                    print "Building Docker images..."
                    // ใช้ docker-compose เพื่อ build Docker image
                    sh 'docker-compose -f docker-compose.yml build'
                    print "Docker image build completed."
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    print "Deploying Docker containers..."
                    // ใช้ docker-compose เพื่อรัน container
                    sh 'docker-compose -f docker-compose.yml up -d'
                    print "Docker containers are running."
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Build and deployment successful.'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
