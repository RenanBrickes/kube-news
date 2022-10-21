pipeline {
    // Quem vai execultar a aplicação
    agent any

    // Stage -> Estagios a serem execultada
    stages {
        // Cria primeiro estagio a ser execultado
        stage("Build Docker Image") {
            // Declaração de passo a passo estagio
            steps{
                // Gera uma imagem docker da aplicação
                script {
                    dockerapp = docker.build("renanbrickes/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
        stage("Push Docker Image") {
            
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com','dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }

        stage("Deploy Kubernetes") {
            environment {
                tag_version = "${env.BUILD_ID}"
            }
            steps {
                withKubeConfig([credentialsId: 'kube_config']) {
                    sh 'sed -i "s/{{TAG}}/$tag_version/g" ./k8s/deployment.yaml'
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
    }
}
