pipeline {
     agent any

   environment {
	DOCKER_PASSWORD=credentials('5468209a-cd1d-46ea-95d9-5721f390d90b')
  }		
    stages{
        stage('cloning the Git Repo') {
            steps {
                sh '''
                git clone https://github.com/Abdul8057/express.git
		rm -rf express
                '''
            }
        }
        stage('Building the docker image') {
            steps {
                sh '''
                docker build . -t hello-world:${BUILD_NUMBER}
		docker tag hello-world:${BUILD_NUMBER} abdul8057/hello-world:${BUILD_NUMBER}
                '''
            }
        }
        stage('Push Docker Image'){
            steps{
               sh ''' 
	       echo ${DOCKER_PASSWORD} | docker login -u abdul8057 --password-stdin 
               docker push abdul8057/hello-world:${BUILD_NUMBER}
             '''
            }
        }
	stage('Running the Docker Image with port 3000'){
            steps{
               sh ''' 
	       docker run -it -d Ubuntu:latest
	       docker rm -f $(docker ps -a -q) 
	       docker run -it -d -p 3000:3000 hello-world:${BUILD_NUMBER}
             '''
            }
        }    
    }
}
