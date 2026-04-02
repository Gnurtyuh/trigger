pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
            }
        }
    }
    
    post {
        success {
            echo 'Build thành công!'
            // Dùng mail thay vì emailext
            mail (
                to: 'nkocsoc2004@gmail.com',
                subject: "✅ BUILD SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thành công.\n\nChi tiết: ${env.BUILD_URL}"
            )
        }
        failure {
            echo 'Build thất bại!'
            mail (
                to: 'nkocsoc2004@gmail.com',
                subject: "🚨 BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thất bại.\n\nVui lòng kiểm tra: ${env.BUILD_URL}"
            )
        }
    }
}
