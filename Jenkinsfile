pipeline {
    environment {
        registry = "registry.hub.docker.com/aswinmkolathur/jenkins4"
        dockerImage = 'flask-app' 
    }
    agent any
    
    stages { 
        stage('Cloning our Git') { 
            steps { 
                script {
                    url: 'https://github.com/aswin219/jenkins4.git' 
                }
            }
        } 
        
        stage('Building our image') { 
            steps { 
                script { 
                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 
                }
            } 
        }
        stage('Deploy our image') { 
            steps { 
                script { 
                    docker.withRegistry( 'https://registry.hub.docker.com', 'dockerhub_id' ) { 
                        dockerImage.push() 
                    }
                } 
            }
        } 
        stage('Cleaning up') { 
            steps { 
                sh "docker rmi $registry:$BUILD_NUMBER" 
            }
        } 
    }
}
