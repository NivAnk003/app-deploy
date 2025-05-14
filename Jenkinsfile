pipeline {
    agent any

    environment {
        TARGET_HOST = 'ubuntu@3.110.131.113'
        SSH_KEY = 'target-ec2-ssh'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/NivAnk003/app-deploy.git'
            }
        }

        stage('Deploy to Target EC2') {
            steps {
                sshagent(credentials: [env.SSH_KEY]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no $TARGET_HOST << 'EOF'
                      cd ~/sample-app
                      chmod +x deploy.sh
                      ./deploy.sh
                    EOF
                    """
                }
            }
        }
    }
}

