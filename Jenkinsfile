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
                    echo "Cloning repository..."
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: 'c6b18afc-c59c-488d-8e79-cc9b5250bad7',
                            url: 'https://github.com/AnemoneTK/Trainify-Test-Jenkins.git'
                        ]]
                    ])
                    echo "Repository cloned successfully."
                }
            }
        }
         stage('Check Docker Compose Version') {
            steps {
                script {
                    echo "Checking Docker Compose version..."
                    // ตรวจสอบ Docker Compose เวอร์ชัน
                    sh 'docker-compose --version'
                }
            }
        }

         stage('Build') {
            steps {
                script {
                    echo "Current directory: ${pwd()}"
                    echo "Listing files:"
                    sh 'ls -l'
                    echo "Building Docker image..."
                    // เพิ่ม flag --no-cache เพื่อหลีกเลี่ยงการใช้ cache ในการ build
                    sh "docker-compose -f ${env.DOCKER_COMPOSE_FILE} build --no-cache"
                    echo "Docker image build complete."
                }
            }
        }


        stage('Deploy') {
            steps {
                script {
                    // ใช้คำสั่ง docker-compose เพื่อ deploy container
                    sh "docker compose -f ${env.DOCKER_COMPOSE_FILE} up -d"
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Build and deploy completed successfully!'
        }
        failure {
            echo 'Build or deploy failed!'
        }
    }
}