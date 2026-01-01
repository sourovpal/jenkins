pipeline {
    agent any

    parameters {
        choice(
            name: 'GIT_BRANCH',
            choices: ['main', 'dev', 'deploy'],
            description: 'Select Git branch to build'
        )
    }

    stages {
        stage('Build & Restart Deployment') {
            steps {
                echo 'Starting deployment restart...'

                sh '''
                    ssh -o StrictHostKeyChecking=no \
                    -i /var/jenkins_home/.ssh/id_rsa \
                    sourov@172.17.186.110 "
                        set -e
                        cd ~/www
                        echo 'Using Minikube Docker...'

                        source ~/.bashrc || true
                        eval \\$(minikube docker-env)

                        echo 'Building Docker image...'
                        docker build -t html-website:latest .

                        echo 'Restarting deployment...'
                        kubectl rollout restart deployment/html-website-deployment

                        echo 'Waiting for rollout...'
                        kubectl rollout status deployment/html-website-deployment

                        echo 'Cluster status:'
                        kubectl get all
                    "
                '''
            }
        }

        stage('Post-Check') {
            steps {
                echo 'Deployment restarted successfully ✅'
            }
        }        
    }

    post {
        success {
            echo 'Build successfully ✅'
        }
        failure {
            echo 'Build failed ❌'
        }
    }
}
