pipeline {
    agent any

    environment {
        APP_NAME = 'apachewebsite'
        SERVER_IP = '35.154.226.86' // Apache web server IP
        DEPLOY_DIR = '/var/www/html' // Path where the website files will be deployed on the server
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from GitHub repository
                git 'https://github.com/akshu20791/apachewebsite.git'
            }
        }

      
        stage('Deploy') {
            steps {
                echo 'Deploying application to Apache server...'
                // Deploy the application to Apache web server using SSH
                sh '''
                    ssh -o StrictHostKeyChecking=no user@$SERVER_IP << 'EOF'
                    rm -rf $DEPLOY_DIR/*  # Remove old files
                    cp -r * $DEPLOY_DIR/   # Copy new files
                    sudo systemctl restart apache2  # Restart Apache to apply changes
                    EOF
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
