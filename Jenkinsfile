def ecrurl = "757113113577.dkr.ecr.us-east-1.amazonaws.com/ubuntu16.04"
def imagename = "ubuntu:16"
def container = "apache2"
node {
   echo 'Building Apache Docker Image'

stage('Git Checkout') {
    git 'https://github.com/amarsingh3d/jenkins-pipeline'
    }
    
stage('Build Docker Imagae'){
     powershell "docker build -t  ${imagename} ."
    }
    
stage('Stop Existing Container'){
     powershell "docker stop ${container}"
    }
    
stage('Remove Existing Container'){
     powershell "docker rm ${container}"
    }
    
stage ('Runing Container to test built Docker Image'){
    powershell "docker run -dit --name ${container} -p 80:80 ${imagename}"
    }
    
stage('ECS Tag Image'){
    powershell "docker tag ${imagename} ${ecrurl}"
    }

stage('ECS Push'){i
    docker.withRegistry('https://757113113577.dkr.ecr.us-east-1.amazonaws.com', 'ecr:us-east-1:ECR-access') {

    docker.image("${ecsurl}").push()
   }
    }

}
