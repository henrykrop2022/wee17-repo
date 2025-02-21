pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/henrykrop2022/wee17-repo.git' // Update with your repo URL
        WORK_DIR = '/home/ec2-user/cicd-pipeline' // Directory on the Ansible master
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
    }
}