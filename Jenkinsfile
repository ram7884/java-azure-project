pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
              git 'https://github.com/ram7884/java-azure-project.git'
            }
        }
        stage('build') {
            steps {
              sh "mvn clean package"
            }
        }
    }
}
