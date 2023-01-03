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

        stage('Deploy To Staging') { 
            steps {
                sh 'ssh -o StrictHostKeyChecking=no deployment-user@192.168.56.111 "source venv/bin/activate; \
                cd polling; \
                git pull origin master; \
                pip install -r requirements.txt --no-warn-script-location; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restart gunicorn "'
                // 
            }
        }

        stage('Deploy To Production') { 

            input {
                message "Shall we deploy to production?"
                ok "YES Please!"
            }
            steps {
                sh 'ssh -o StrictHostKeyChecking=no deployment-user@192.168.56.108 "source venv/bin/activate; \
                cd polling; \
                git pull origin master; \
                pip install -r requirements.txt --no-warn-script-location; \
                python manage.py migrate; \
                deactivate; \
                sudo systemctl restart nginx; \
                sudo systemctl restart gunicorn "'
                // 
            }
        }
    }
}