pipeline {

    agent any // defini qual agente irá executar o pipeline. any -> primeiro ambiente disponível (Jenkins Master - Própria máquina)

    stages {
        stage('Clean') {
            steps {
                sh "./mvnw clean"
            }
        }
        stage("Build") {
            steps {
                sh "./mvnw package"
            }
        }
        stage('Test') {
            steps {
                sh "./mvnw test"
            }
        }
        stage('JaCoCo') {
            steps {
                echo 'Code Coverage'
                jacoco()
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t brunosilva1988/eureka .'
            }
        }
        stage('Push image') {
            withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'brunosilva1988', passwordVariable: 'bts09081988')]) {
                def registry_url = "registry.hub.docker.com/"
                bat "docker login -u $USER -p $PASSWORD ${registry_url}"
                do  cker.withRegistry("http://${registry_url}", "docker-hub-credentials") {
                    sh 'docker push brunosilva1988/eureka'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh "docker stack deploy --compose-file docker-compose.yml store"
            }
        }
    }
}