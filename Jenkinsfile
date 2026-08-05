pipeline {
    agent any
    stages {
        stage('Code') {
            steps {
                echo 'Copy the code'
                git url: "https://github.com/Mohitxjoshii/django-notes-app.git", branch: "main"
            }
        }
        stage('Build') {
            steps {
                echo 'Building the code'
                sh "docker build -t django-notes-app ."
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing the code to Docker Hub'
                withCredentials([usernamePassword(credentialsId: "dockerHub", passwordVariable: "dockerPass", usernameVariable: "dockerUser")]) {
                    sh "docker login -u ${dockerUser} -p ${dockerPass}"
                    sh "docker tag django-notes-app ${dockerUser}/django-notes-app:latest"
                    sh "docker push ${dockerUser}/django-notes-app:latest"
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the code'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the application'
            }
        }
    }
}
