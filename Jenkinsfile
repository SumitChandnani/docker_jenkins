pipeline{
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'subhankar720', url: 'https://github.com/subhankar720/docker_jenkins.git']]])

                sh "mvn -Dmaven.test.failure.ignore=true clean package"
                
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                  sh 'docker build -t subhankar720/docker_jenkins:latest .'
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                 docker login -u subhankar720 -p Mini@2000
                     sh 'docker push subhankar720/docker_jenkins:latest' 
                 
                }
            }
        }
    }
    
}