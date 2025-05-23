pipeline {
    agent any

    environment {
        GIT_REPO_URL = 'https://github.com/vikasxjha/aws-materials.git'
        GIT_BRANCH = 'main'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${env.GIT_BRANCH}",
                    url: "${env.GIT_REPO_URL}"
            }
        }

        stage('List Files') {
            steps {
                script {
                    sh 'echo "Listing all files in the repository:"'
                    sh 'find . -type f'
                }
            }
        }
    }
}
