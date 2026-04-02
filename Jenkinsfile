pipeline {
    agent any
    
    environment {
        // Định nghĩa email recipients
        DEV_TEAM = 'dev-team'
        QA_TEAM = 'qa-team'
    }
    
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
                to: "${env.DEV_TEAM}",
                subject: "✅ BUILD SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} đã thành công.
                    
                    Chi tiết: ${env.BUILD_URL}
                    
                    Commit: ${env.GIT_COMMIT}
                    Branch: ${env.GIT_BRANCH}
                """,
                mimeType: 'text/html',
                from: 'jenkins@yourcompany.com'
            )
        }
        
        failure {
            echo 'Build thất bại!'
            emailext (
                to: "${env.DEV_TEAM}, ${env.QA_TEAM}",
                subject: "🚨 BUILD FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    <h2>Build thất bại!</h2>
                    <p>Build <b>${env.BUILD_NUMBER}</b> của job <b>${env.JOB_NAME}</b> đã thất bại.</p>
                    <p>Vui lòng kiểm tra chi tiết tại: <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>
                    <hr/>
                    <p><b>Logs (trích xuất):</b></p>
                    <pre>${currentBuild.rawBuild.getLog(50)}</pre>
                """,
                mimeType: 'text/html',
                from: 'jenkins@yourcompany.com',
                attachLog: true
            )
        }
        
        unstable {
            echo 'Build không ổn định!'
            emailext (
                to: "${env.DEV_TEAM}",
                subject: "⚠️ BUILD UNSTABLE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    Build ${env.BUILD_NUMBER} của job ${env.JOB_NAME} không ổn định (test fails).
                    Chi tiết: ${env.BUILD_URL}
                """,
                mimeType: 'text/plain',
                from: 'jenkins@yourcompany.com'
            )
        }
        
        changed {
            echo 'Trạng thái build đã thay đổi so với lần trước!'
        }
    }
}
