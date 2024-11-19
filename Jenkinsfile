pipeline {
    agent any

    tools{
        jdk 'jdk'
        maven 'maven3'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/amt-fredrick-amoako/Java-AL-W4-CICD.git'
            }
        }
        stage('Compile') {
            steps{
                sh "mvn compile"
            }

        }
        stage('Test') {
            steps {
                 sh "mvn test"
            }
        }
        stage('Build') {
            steps {
                 sh "mvn package"
            }
        }
        stage('Build & Tag Docker Image') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                        sh "docker build -t fredamoako/Java-AL-W4-CICD:latest ."
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                        sh "docker push fredamoako/Java-AL-W4-CICD:latest"
                    }
                }
            }
        }
//         stage('Deploy K8 Clusters'){
//             steps{
//                 sh "kubectl apply -f devops.yml"
//             }
//         }
    }
}