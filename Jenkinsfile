pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                sh 'docker build -f Dockerfile . -t ahmedalaa14/jenkins:v1.0'
            }
        }
        stage('artifact') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'DockerHub-Credential', passwordVariable: 'pass', usernameVariable: 'username')]){
                sh 'docker login -u ${username} -p ${pass}'
                sh 'docker push ahmedalaa14/jenkins:v1.0'
            }
           }
        }
        stage('deploy') {
            steps {
                sh 'docker run -d -p 3000:3000 ahmedalaa14/jenkins:v1.0'
            }
        }
    }
}