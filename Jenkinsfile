pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Terraform Provisioning') {
            steps {
                dir('terraform') {
                    script {
                        def terraformCommand = 'terraform'

                        // Terraform initialization and apply
                        sh "${terraformCommand} init"
                        sh "${terraformCommand} apply -auto-approve"
                    }
                }
            }
        }

        stage('Ansible Configuration') {
            steps {
                dir('ansible') {
                    script {
                        def ansibleCommand = 'ansible-playbook'

                        // Dynamic Inventory Script
                        sh "${ansibleCommand} -i ../terraform_inventory.py playbook.yml"
                    }
                }
            }
        }
    }

    post {
        always {
            // Cleanup or notification tasks
        }
    }
}
}
