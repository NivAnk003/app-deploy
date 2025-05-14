pipeline {
    agent any

    environment {
        TARGET_HOST = 'ubuntu@3.110.131.113'
        SSH_KEY = 'target-ec2-ssh'  // Jenkins credentials ID
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/NivAnk003/app-deploy.git/'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sshagent(credentials: [env.SSH_KEY]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no $TARGET_HOST << 'EOF'
                      chmod +x ~/deploy.sh
                      ~/deploy.sh
                    EOF
                    """
                }
            }
        }
    }
}
