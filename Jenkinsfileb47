pipeline {
    agent any

    stages {
        stage('SCM') {
            steps {
               git 'https://github.com/Kumarbgm16/java-azure-project.git' 
            }
        }
    stage('Package') {
            steps {
               sh 'mvn clean package' 
            }
        }
    stage('Build Docker OWN image') {
            steps {
                sh "sudo docker build -t learndevops16/javasantaapp:latest ."

            }
        }
      stage('docker push ') {
     steps {
     withCredentials([string(credentialsId: 'DOCKER_HUB_PWD', variable: 'DOCKER_HUB_PASS_CODE')])  {
    // some block
        sh "sudo docker login -u learndevops16 -p $DOCKER_HUB_PASS_CODE"
        }
        sh "sudo docker push learndevops16/javasantaapp:latest"
        }
        }    
        stage('Deploy webAPP in Prod Env') {
    steps {
    sshagent(['17b49d23-0439-450f-9185-db74dd1f7e6f']) {
    sh "ssh -o StrictHostKeyChecking=no ubuntu@13.126.118.135   sudo wget https://raw.githubusercontent.com/Kumarbgm16/java-azure-project/master/k8-dep-svc.yml"    
    sh "ssh -o StrictHostKeyChecking=no ubuntu@13.126.118.135   sudo kubectl apply -f k8-dep-svc.yml"
}
}
}
    }
}
