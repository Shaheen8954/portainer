pipeline {
    agent any

    stages {
         stage('Hello') {
            steps {
               echo 'hello'
            }
        }
        stage('cleanup workspace') {
            steps {
                cleanWs()
            }
        }
         stage('clone code') {
            steps {
               checkout scm
            }
        }
        stage('stop $ remove container') {
            steps {
               sh "docker stop portainer; docker rm portainer"
               sh "docker volume rm portainer_data portainer_portainer_data"
            }
        }
        stage('run container') {
            steps {
                sh """
                docker run -d \
                -p 8000:8000 \
                -p 9443:9443 \
                --name portainer \
                -v /var/run/docker.sock:/var/run/docker.sock \
                -v portainer_data:/data \
                 portainer/portainer-ce:lts
                """
            }
        }
    }
}

