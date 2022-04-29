pipeline {
    agent any
    
    parameters {
         choice choices: ['qa', 'production'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
       }

    stages {
        stage('Copy artifact') {
            steps {
                copyArtifacts filter: 'sample', fingerprintArtifacts: true, projectName: 'sample_pipeline', selector: lastSuccessful()
            }
        }
        stage('Deliver') {
            steps {
              sshagent(['vagrant']) {
                  sh 'ansible-playbook -i ${DEPLOY_TO}.ini playbook.yml'
              }
            }
        }
    }
}
