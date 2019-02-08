def ecrurl = "757113113577.dkr.ecr.us-east-1.amazonaws.com/ubuntu16.04"
def imagename = "ubuntu:16"
def container = "apache2"
node {
   echo 'Building Apache Docker Image'

stage('Git Checkout') {
    git 'https://github.com/amarsingh3d/jenkins-pipeline-ecr'
    }
    
stage('Build Docker Imagae'){
     sh label: '', script: "sudo docker build -t ${imagename} ."
    }

stage('Stop Existing Container'){
     sh label: '', script: "sudo docker stop ${container}"
    }	
	
stage ('Runing Container to test built Docker Image'){
    sh label: '', script: "sudo docker run -dit --rm --name ${container} -p 80:80 ${imagename}"
    }
    
stage('Tag Docker Image'){
    sh label: '', script: "sudo docker tag ${imagename} ${env.dockeruser}/ubuntu:16.04"

stage('ECR Push'){
    docker.withRegistry('https://757113113577.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:ECR-Access') {
    sh label: '', script: "sudo docker push ${ecrurl}"
	}
	}
}
}
