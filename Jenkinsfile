pipiline {

    // Quem vai execultar a aplicação
    agent any

    // Stage -> Estagios a serem execultada
    stages {
        // Cria primeiro estagio a ser execultado
        stage("Build Docker Image") {
            // Declaração de passo a passo estagio
            steps{
                script {
                    dockerapp = docker.build("renanbrickes/kube-news:${env.BUILD.ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
    }
}