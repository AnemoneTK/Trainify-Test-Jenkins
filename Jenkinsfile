pipeline {
    agent any
    environment {
        // ระบุ path ของไฟล์ docker-compose.yml
        DOCKER_COMPOSE_FILE = "docker-compose.yml"
    }

    stages {
        stage('Clone Repository') {
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

        stage('Build Docker Containers') {
            steps {
                script {
                    print "Building Docker containers using docker-compose..."
                    // ใช้ docker-compose ในการ build containers ตามที่กำหนดใน docker-compose.yml
                    sh 'docker-compose -f ${DOCKER_COMPOSE_FILE} build'
                    print "Docker build completed successfully."
                }
            }
        }

        stage('Deploy Docker Containers') {
            steps {
                script {
                    print "Deploying Docker containers..."
                    // ใช้ docker-compose เพื่อเริ่ม container
                    sh 'docker-compose -f ${DOCKER_COMPOSE_FILE} up -d'
                    print "Docker containers are up and running."
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Docker containers built and deployed successfully.'
        }
        failure {
            echo 'Build or deployment failed.'
        }
    }
}
