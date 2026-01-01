pipeline {
    agent any

    stages {
        stage('Restart Deployment') {
            steps {
                echo 'Starting deployment restart...'

                sh """
                    ssh -t -i /var/jenkins_home/.ssh/id_rsa -o StrictHostKeyChecking=no sourov@172.17.186.110 '
                        eval $(minikube docker-env) &&
                        docker build -t html-website:latest && 
                        kubectl rollout restart deployment/html-website-deployment
                    '
                """
            }
        }

        stage('Post-Check') {
            steps {
                echo 'Deployment restarted, checking status...'
            }
        }
    }
}
