pipeline {

    agent any
        
    

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Image') {
            steps {
                script {
                    myapp = docker.build("apg8501/node-api:${env.BUILD_ID}")
                }
            }
        }
        stage('pushing images to dockerhub'){
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerlogin') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        
    }
}
