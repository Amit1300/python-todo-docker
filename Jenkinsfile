pipeline {
    agent {
        label 'dev'
    }
    
    stages {
        stage("clone code") {
            steps {
                echo "cloning"
                git url: "https://github.com/Amit1300/python-todo-docker.git", branch: "main"
            }
        }
        stage("build") {
            steps {
                sh "docker build -t amit1300/todo:${env.BUILD_NUMBER} . "
            }
        }
        stage("push") {
            steps {
                withCredentials([usernamePassword(credentialsId: "docker_login", passwordVariable: "password", usernameVariable: "docker_user")]) {
                    sh "docker login -u ${env.docker_user} -p ${env.password}"
                    sh "docker push amit1300/todo:${BUILD_NUMBER}"
                }
            }
        }
    }
}

