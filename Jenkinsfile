pipeline {
    agent any 

    environment {
        GIT_REPO = 'Github-repo-link'
        SSH_CREDENTIALS_ID = 'SSH-CREDENTIALS-ID' 
        VM_TARGET_PATH = '/PathToDirectory' 
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: GIT_REPO
            }
        }

        stage('Copy Repository to VM') {
            steps {
                sshagent([SSH_CREDENTIALS_ID]) {
                    sh """
                        scp -r ./* user@VM-IP:${VM_TARGET_PATH}
                    """ 
                }
            }
        }

        stage('Post Actions') {
            steps {
                echo 'Repository has been copied to the VM.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
