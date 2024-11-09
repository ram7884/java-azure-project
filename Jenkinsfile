pipeline {
    agent any

    stages {
        stage('clone the repo') {
            steps {
            git 'https://github.com/Kumarbgm16/java-azure-project.git'
            }
        }
     stage('build the project') {
            steps {
            sh 'mvn clean package'
            }
        }
    stage('create the docker image') {
            steps {
            sh 'sudo docker build -t saidevops16/webappdemob49:latest .'
            }
        }
        stage('docker push ') {
     steps {
     withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'DOCKER_HUB_PASS_CODE')])  {
    // some block
        sh "sudo docker login -u saidevops16 -p $DOCKER_HUB_PASS_CODE"
        }
        sh "sudo docker push saidevops16/webappdemob49:latest"
        }
        }  
        
        stage('Deploy to docker Env') {
steps {
        sh "sudo docker rm -f app3" 
    sh "sudo docker run -itd --name app3 -p 9000:8080 saidevops16/webappdemob49:latest" 

}
}
 stage('Deploy webAPP in kube Env') {
    steps {
    sshagent(['QA']) {
         sh "ssh -o StrictHostKeyChecking=no ubuntu@65.0.45.74  sudo kubectl delete -f k8-dep-svc.yml"
    sh "ssh -o StrictHostKeyChecking=no ubuntu@65.0.45.74     sudo wget https://raw.githubusercontent.com/Kumarbgm16/java-azure-project/master/k8-dep-svc.yml"    
    sh "ssh -o StrictHostKeyChecking=no ubuntu@65.0.45.74     sudo kubectl apply -f k8-dep-svc.yml"
}
}
}        
    }
}
