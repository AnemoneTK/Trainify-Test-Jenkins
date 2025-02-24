pipeline {
    agent any
    // environment {
    //     // ระบุ path ของไฟล์ docker-compose.yml
    //     DOCKER_COMPOSE_FILE = "docker-compose.yml"
    // }

    stages {
        stage('Clone Repository') {
            steps{
                print "Cloning repository..."
                checkout([
                        $class : 'GitSCM',
                        branches : [[name : '*/main']],
                        userRemoteConfigs :[[
                            credentialsId: '76fb8aa3-686a-47ae-863a-772e8e12c160',
                            // credentialsId: 'c6b18afc-c59c-488d-8e79-cc9b5250bad7',
                            url: 'https://github.com/AnemoneTK/Trainify-Test-Jenkins.git'
                        ]]
                    ])
                print "Clone Success"
            }
        }
        //  stage('Check Docker Compose Version') {
        //     steps {
        //         script {
        //             echo "Checking Docker Compose version..."
        //             sh 'docker-compose --version'
        //         }
        //     }
        // }

        // stage('Build') {
        //     steps {
        //         script {
        //             echo "Current directory: ${pwd()}"
        //             echo "Listing files:"
        //             sh 'ls -l'
        //             echo "Building Docker image..."
        //             // เพิ่ม flag --no-cache เพื่อหลีกเลี่ยงการใช้ cache ในการ build
        //             sh "docker-compose -f ${env.DOCKER_COMPOSE_FILE} build --no-cache"
        //             echo "Docker image build complete."
        //         }
        //     }
        // }

        // stage('Deploy') {
        //     steps {
        //         script {
        //             // ใช้คำสั่ง docker-compose เพื่อ deploy container
        //             sh "docker compose -f ${env.DOCKER_COMPOSE_FILE} up -d"
        //         }
        //     }
        // }
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