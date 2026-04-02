pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // git 'https://github.com/your-repo.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building application...'
                // sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                // sh 'mvn test'
            }
        }
    }

    post {
        always {
            echo 'Pipeline hoàn tất - đây là bước luôn chạy dù thành công hay thất bại'
        }
        success {
            echo 'Build thành công!'
            emailext (
                to: 'nkocsoc2004@gmail.com',  // Email nhận

                subject: "✅ BUILD SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thành công.\n\nChi tiết: ${env.BUILD_URL}",
                from: 'nkocnox2004@gmail.com'  // Email gửi
            )
        }
        failure {
            echo 'Build thất bại!'
            emailext (
                to: 'nkocsoc2004@gmail.com',  // Email nhận
                subject: "🚨 BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thất bại.\n\nVui lòng kiểm tra: ${env.BUILD_URL}",
                from: 'nkocnox2004@gmail.com',  // Email gửi
                attachLog: true
            )
        }
        unstable {
            echo 'Build không ổn định!'
            emailext (
                to: 'nkocsoc2004@gmail.com',
                subject: "⚠️ BUILD UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} không ổn định.\n\nChi tiết: ${env.BUILD_URL}",
                from: 'nkocnox2004@gmail.com'
            )
        }
        changed {
            echo 'Trạng thái build đã thay đổi so với lần trước!'
        }
    }
}
