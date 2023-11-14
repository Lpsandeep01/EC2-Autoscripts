pipeline {
    agent any

    environment {
        ANSIBLE_PLAYBOOK = "/home/ansible-playbooks"
        INVENTORY_FILE = "/home/ansible-playbooks/inventory.ini"
       PRIVATE_KEY = "~/.ssh/key.pem"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    ansiblePlaybook = sh(script: 'which ansible-playbook', returnStatus: true).trim()
                    if (ansiblePlaybook == 1) {
                        error("ansible-playbook not found. Please make sure Ansible is installed on your Jenkins agent.")
                    }

                    sh """
                        ${ANSIBLE_PLAYBOOK} -i ${INVENTORY_FILE} /home/ansible-playbooks/ansible-playbook.yml --private-key=${PRIVATE_KEY}
                    """
                }
            }
        }
    }
}
