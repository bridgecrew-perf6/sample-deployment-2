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
              withCredentials([sshUserPrivateKey(credentialsId: "vagrant-private-key", keyFileVariable: 'keyfile')])
                  sh 'scp -o "StricHostKeyChecking=no" -i ${keyfile} ./sample vagrant@10.10.50.3:'
            }
        }
    }
}
