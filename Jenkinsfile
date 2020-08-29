pipeline {
   agent any
   stages {
     stage('pull repo'){
    	steps {
          git 'https://github.com/karthik0248/ngnix-repo1.git'
        }
     }
     stage('pull master'){
    	steps {
          sh 'git pull origin master'
        }
     }
     stage('docker version check'){
       steps{
          echo 'docker version check'
          sh 'docker --version'
       }
     }
     stage('docker build image'){
       steps{
          echo 'docker build image'
          sh 'docker build -t myng:1 .'
       }
     }
     stage('Push to ECR'){
       steps{
          sh 'docker build -t myng:1 .'
          sh '$(aws ecr get-login --no-include-email)'
          sh 'docker tag myng:1 587589636093.dkr.ecr.us-east-1.amazonaws.com/myng:1'
          sh 'docker push 587589636093.dkr.ecr.us-east-1.amazonaws.com/myng:1'
       }
     }
     stage('ping to docker'){
       steps{
          sh 'ansible docker -m ping'
       }
     }
     stage('start containerr'){
       steps{
          sh 'ansible-playbook dockercon.yml --syntax-check'
          sh 'ansible-playbook dockercon.yml'
       }
     }
   }
}
