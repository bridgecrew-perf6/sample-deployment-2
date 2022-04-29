pipeline {
    agent any
    
    parameters {
         choice choices: ['qa', 'production', 'cloud'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
       }

    stages {
        stage('Copy artifact') {
            steps {
                copyArtifacts filter: 'sample', fingerprintArtifacts: true, projectName: 'sample_pipeline', selector: lastSuccessful()
            }
        }
        stage('Deliver') {
            steps {
              withCredentials([sshUserPrivateKey(credentialsId: "vagrant", keyFileVariable: 'keyfile')]) {
                  sh 'ansible-playbook --private-key=${keyfile} -i ${DEPLOY_TO}.ini playbook.yml'
              }
            }
        }
    }
}
