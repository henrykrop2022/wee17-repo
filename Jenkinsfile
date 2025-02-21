pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/henrykrop2022/wee17-repo.git' // Update with your repo URL
        WORK_DIR = '/home/ec2-user/ansible-dev' // Directory on the Ansible master
    }
    stages {
        stage('Clone Ansible Playbook') {
            steps {
                git branch: 'main', url: 'https://github.com/henrykrop2022/wee17-repo.git'
            }
        }
        stage('Sync Playbook to Ansible Master') {
            steps {
                sh """
                    rsync -avz -e "ssh -o StrictHostKeyChecking=no" * ec2-user@ip-172-31-33-45:${WORK_DIR}/
                """
            }
        }
         stage('Execute Ansible Playbook') {
            steps {
                sh """
                    ssh ec2-user@ip-172-31-33-45 '
                    cd ${WORK_DIR} &&
                    ansible-playbook -i  play4.yml '
                """
            }
        }
     }
}
