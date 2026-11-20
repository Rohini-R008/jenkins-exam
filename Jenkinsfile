pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Build stage: installing dependencies...'
                sh 'pip3 install --break-system-packages -r requirements.txt || pip3 install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                echo 'Test stage: running unit tests...'
                sh 'python3 -m unittest discover -s .'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy stage: copying app to deploy directory...'
                sh '''
                mkdir -p ${WORKSPACE}/deploy
                cp ${WORKSPACE}/app.py ${WORKSPACE}/deploy/
                echo "Deployed files:"
                ls -l ${WORKSPACE}/deploy
                '''
            }
        }
    }
    post {
        success { echo 'Pipeline completed successfully!' }
        failure { echo 'Pipeline failed. Check logs.' }
    }
}