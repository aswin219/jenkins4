pipeline {
    environment {
        registry = "aswinmkolathur/jenkins4"
        registryCredential = 'dockerhub_id'
        dockerImage = '' 
    }
    agent any
    
    stages { 
        stage('Cloning our Git') { 
            steps {
                git 'https://github.com/aswin219/jenkins4.git'                 
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
                    docker.withRegistry( '', registryCredential ) { 
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
