pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/ltryash/apachewebsite.git'
            }
        }

        stage('Deploy to Apache Server') {
            steps {
                script {
                    // Ensure /var/www/html exists and clear old files
                    sh '''
                    sudo rm -rf /var/www/html/*
                    sudo cp -r * /var/www/html/
                    sudo chown -R www-data:www-data /var/www/html/
                    sudo chmod -R 755 /var/www/html/
                    '''
                }
            }
        }

        stage('Restart Apache') {
            steps {
                script {
                    sh 'sudo systemctl restart apache2'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful! Website is live on Apache.'
        }
        failure {
            echo 'Deployment Failed! Check the logs for errors.'
        }
    }
}
