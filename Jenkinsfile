pipeline {
    agent any
    stages {
        
        stage('Deploy to Remote Server via ansible') {
            environment {
                ip_address = '51.20.95.8'
                ssh_user = 'ubuntu'
                dist_path = '/home/ubuntu'
                ssh_key_path = '/home/ubuntu/.ssh/id_ed25519'
                ansible_command = 'ansible-playbook -i inventory_aws_ec2.yml first-playbook.yml'
            }
            steps {
                sshagent(['ansible-ssh']) {
                    sh 'echo "Running commands on remote server..."'
                    sh "scp -o StrictHostKeyChecking=no  docker-compose.yml ansible/* ${ssh_user}@${ip_address}:${dist_path}"
                    withCredentials([sshUserPrivateKey(credentialsId: 'ansible-ssh', keyFileVariable: 'SSH_KEY')]) {
                        sh "scp  $SSH_KEY ${ssh_user}@${ip_address}:${ssh_key_path}"
                    }
                    sh "ssh ${ssh_user}@${ip_address} ${ansible_command}"
                }
            }
        }
    }
}