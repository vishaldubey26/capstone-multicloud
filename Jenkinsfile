pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vishaldubey26/capstone-multicloud.git'
            }
        }
        stage('Deploy to AWS') {
            steps {
                sh '''
                    scp -o StrictHostKeyChecking=no -i /var/lib/jenkins/.ssh/capstone Task-1/aws/index-aws.html ubuntu@44.223.16.81:/tmp/
                    ssh -o StrictHostKeyChecking=no -i /var/lib/jenkins/.ssh/capstone ubuntu@44.223.16.81 "sudo cp /tmp/index-aws.html /var/www/html/ && sudo systemctl restart nginx"
                '''
            }
        }
        stage('Deploy to Azure') {
            steps {
                sh '''
                    scp -o StrictHostKeyChecking=no -i /var/lib/jenkins/.ssh/capstone Task-1/azure/index-azure.html azureuser@20.197.8.180:/tmp/
                    ssh -o StrictHostKeyChecking=no -i /var/lib/jenkins/.ssh/capstone azureuser@20.197.8.180 "sudo cp /tmp/index-azure.html /var/www/html/ && sudo systemctl restart nginx"
                '''
            }
        }
    }
    post {
        success { echo 'Deployment successful!' }
        failure { echo 'Deployment failed!' }
    }
}
