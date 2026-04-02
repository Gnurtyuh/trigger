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
                // sh 'mvn clean compile' hoặc tương đương
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
                subject: "✅ BUILD SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thành công.",
                to: 'dev-team@yourcompany.com'
            )
        }
        failure {
            echo 'Build thất bại!'
            emailext (
                subject: "🚨 BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thất bại. Vui lòng kiểm tra: ${env.BUILD_URL}",
                to: 'dev-team@yourcompany.com, qa-team@yourcompany.com',
                attachLog: true
            )
        }
        unstable {
            echo 'Build không ổn định!'
            emailext (
                subject: "⚠️ BUILD UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} không ổn định.",
                to: 'dev-team@yourcompany.com'
            )
        }
        changed {
            echo 'Trạng thái build đã thay đổi so với lần trước!'
        }
    }
}
