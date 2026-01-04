pipeline {
    agent any

     parameters {
         string(
            name: 'SERVER_USER',
            defaultValue: '',
            description: 'Enter server username...'
        )
         string(
            name: 'SERVER_IP',
            defaultValue: '',
            description: 'Enter server ip address...'
        )
     }

    stages {

        stage('Show Parameters') {
            steps {
                echo "Hello";
                // echo "App Name: ${params.APP_NAME}"
                // echo "Selected Services: ${params.SERVICES}"  // For extended choice
            }
        }

        stage('Test SSH') {
            steps {
                sshagent(['privateKey']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no {params.SERVER_USER}@{params.SERVER_IP} "echo Hello from remote"
                    '''
                }
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
