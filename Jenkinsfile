pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'pip3 install -r requirements.txt'
                // 
            }
        }
        stage('Test') { 
            steps {
                sh 'python3 manage.py test'
                // 
            }
        }
        stage('Deploy') { 
            steps {
                sh 'ssh -o StrictHostKeychecking=no deployment-user@192.168.56.108 "source venv/bin/activate; \
                cd polling; \
                git pull origin master; \
                pip install -r requirement.txt \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restart gunicorn "'
                // 
            }
        }
    }
}