pipeline {
    agent any

    stages {
        stage('List Files') {
            steps {
                sh 'echo "Listing all files in the repository:"'
                sh 'find . -type f'
            }
        }
    }
}
