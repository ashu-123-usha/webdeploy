pipeline {
    agent any

    tools {
        ansible 'ansible'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/ashu-123-usha/webdeploy.git'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                withCredentials([
                    sshUserPrivateKey(
                        credentialsId: 'ansible-ssh-key',
                        keyFileVariable: 'SSH_KEY'
                    )
                ]) {
                    sh '''
                      cp $SSH_KEY /tmp/ssh_key
                      chmod 600 /tmp/ssh_key

                      ansible-playbook \
                        -i inventory/hosts.ini \
                        playbook.yml

                      rm -f /tmp/ssh_key
                    '''
                }
            }
        }
    }
}
