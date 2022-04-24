pipeline {
    agent any

    stages {
        stage('Deliver') {
            steps {
                sh 'scp ./sample vagrant@10.10.50.3'
            }
        }
        stage('Build') {
            steps {
                sh 'go build -o sample main.go'
            }
        }
        stage('Save artifact') {
            steps {
                archiveArtifacts artifacts: 'sample', followSymlinks: false
            }
        }
    }
}
