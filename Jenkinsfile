pipeline {
    agent agent01

    environment {
        IMAGE = "172.23.178.167/demo/nginx:2024-08-23"
        DOCKERFILE = "./Dockerfile"
        DOCKER_IMAGE_REGISTRY_CREDS = credentials('harbor')
    }

    stages {
        stage('Build') {
            steps {
                sh "docker build -t $IMAGE -f $DOCKERFILE ."
            }
        }

        stage('Push') {
            steps {
                sh "docker push $IMAGE"
            }
        }

        stage('Deploy') {
            steps {
                sh "kubectl create deploy demo --image=$IMAGE -n demo"
            }
        }

    }

}
