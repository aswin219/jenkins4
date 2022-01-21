node {
	def app
	def image = 'registry.hub.docker.com/aswinmkolathur/jenkins4'
	def branch = 'main' 
    
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
                    dockerImage = docker.build image + ":$BUILD_NUMBER" 
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
