// Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any // Chạy trên bất kỳ agent nào có sẵn

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo '✅ Đã lấy code từ GitHub.'
            }
        }
        stage('Build') {
            steps {
                echo '🚀 Đang build...'
                // Thêm lệnh build thực tế của bạn ở đây
                sh 'echo "Build thành công"'
            }
        }
        stage('Test') {
            steps {
                echo '🧪 Đang chạy tests...'
                // Thêm lệnh test thực tế của bạn ở đây
                sh 'echo "Tất cả tests passed"'
            }
        }
    }
    post {
        always {
            echo 'Pipeline đã kết thúc.'
        }
        success {
            echo '🎉 Pipeline thành công!'
        }
        failure {
            echo '❌ Pipeline thất bại.'
        }
    }
}