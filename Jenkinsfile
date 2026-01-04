pipeline {
    agent any

     parameters {
        
    }

    stages {

        stage('Show Parameters') {
            steps {
                // echo "App Name: ${params.APP_NAME}"
                // echo "Selected Services: ${params.SERVICES}"  // For extended choice
            }
        }

        stage('Test SSH') {
            steps {
                sshagent(['privateKey']) {
                    // sh '''
                    //     ssh -o StrictHostKeyChecking=no sourov@172.17.186.110 "echo Hello from remote"
                    // '''
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
