pipeline {
    agent any

    environment {
        SONARQUBE_PORT = '9005'
        NGINX_PORT = '90'
        TOMCAT_PORT = '8083'
    }

    stages {
        stage('Start SonarQube') {
            steps {
                sh '''
                docker run -d --name sonar \
                    -p ${SONARQUBE_PORT}:9000 \
                    sonarqube:latest
                '''
            }
        }

        stage('Start NGINX') {
            steps {
                sh '''
                docker run -d --name my-nginx \
                    -p ${NGINX_PORT}:80 \
                    nginx:latest
                '''
            }
        }

        stage('Start Tomcat') {
            steps {
                sh '''
                docker run -d --name my-tomcat \
                    -p ${TOMCAT_PORT}:8080 \
                    tomcat:latest
                '''
            }
        }

        stage('Test Access') {
            steps {
                sh '''
                echo "Access SonarQube at http://localhost:${SONARQUBE_PORT}"
                echo "Access NGINX at http://localhost:${NGINX_PORT}"
                echo "Access Tomcat at http://localhost:${TOMCAT_PORT}"
                '''
            }
        }
    }

    post {
        always {
            sh '''
            echo "Stopping containers..."
            docker rm -f sonar my-nginx my-tomcat || true
            '''
        }
    }
}
