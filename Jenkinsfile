pipeline {
    agent any
    stages {
        stage('Test GitLab') {
            steps {
                retry(3) {
                    script {
                        sh 'curl -I http://job_reset_gitlab_1'
                    }
                }
            }
        }
    }
    post {
        always {
            buildFailureAnalyzer()
        }
    }
}