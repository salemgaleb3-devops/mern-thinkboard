pipeline {
    agent any

    environment {
        DOCKERHUB_USER = "salemghaleb"
        DOCKER_CREDENTIALS = "dockerhub-creds"   
    }

    stages {

        stage('Clone Repository') {
            steps {
                checkout scm
                script {
                    echo "Clone the GitHub repo successfull"
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    echo "Bulilding Docker Images..."
                    sh "docker build -t salemghaleb/mern-backend:${BUILD_NUMBER} ./backend"
                    sh "docker build -t salemghaleb/mern-frontend:${BUILD_NUMBER} ./frontend"
                

                }
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: DOCKER_CREDENTIALS,
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh """
                        echo "${DOCKER_PASS}" | docker login -u "${DOCKER_USER}" --password-stdin
                    """
                }
            }
        }
        stage('Push Image to Docker Hub') {
            steps {
                script {
                    echo "Pushing image to Docker Hub..."
                    sh "docker push salemghaleb/mern-backend:${BUILD_NUMBER}"
                    sh "docker push salemghaleb/mern-frontend:${BUILD_NUMBER}"
                }
            }
        }
        stage('Trigger ManifestUpdate') {
            steps {
                echo "Triggering update manifest job..."
                build job: 'k8supdatemanifest',
                      parameters: [
                        string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)
                      [
            }
        }

    }
    post {
        success {
            echo "Pipeline executed successfully! 🎉"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }




}
