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
              withCredentials([sshUserPrivateKey(credentialsId: "vagrant", keyFileVariable: 'keyfile')]) {
                  sh 'ansible-playbook -private-key=${keyfile} -i hosts.ini playbook.yml'
              }
            }
        }
    }
}
