pipeline {
    agent any
 
    environment {
        EC2_USER = 'ec2-user'                             // or 'ubuntu' for Ubuntu EC2
        EC2_HOST = '13.232.238.240'
        SSH_KEY = '/var/lib/jenkins/webserverkey.pem'        // Jenkins-readable path to your PEM file
        REMOTE_DIR = '/var/www/html'
    }
 
    stages {
        stage('Clone Repository') {
            steps {
                echo "Repository auto-cloned by Jenkins"
            }
        }
 
        stage('Deploy to EC2') {
            steps {
                sh '''
                echo "Deploying static site to EC2..."
 
                scp -i $SSH_KEY -o StrictHostKeyChecking=no -r * $EC2_USER@$EC2_HOST:$REMOTE_DIR
 
                echo "Deployment complete!"
                '''
            }
        }
    }
 
    post {
        success {
            echo "✅ Static website deployed successfully!"
        }
        failure {
            echo "❌ Deployment failed. Check console output."
        }
    }
}
