pipeline {
    agent any

    stages {
        stage('Copy artifact') {
            steps {
                copyArtifacts filter: 'sample', fingerprintArtifacts: true, projectName: 'sample_pipeline', selector: lastSuccessful()
            }
        }
        stage('Deliver') {
            steps {
                sh 'scp ./sample vagrant@10.10.50.3'
            }
        }
    }
}
