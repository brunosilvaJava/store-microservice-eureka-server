pipeline {

    agent any // defini qual agente irá executar o pipeline. any -> primeiro ambiente disponível (Jenkins Master - Própria máquina)

    stages {
        stage('Clean') {
            steps {
                echo "./mvnw clean"
            }
        }
        stage("Build") {
            steps {
                echo "./mvnw package"
            }
        }
        stage('Test') {
            steps {
                echo "./mvnw test"
            }
        }
        stage('JaCoCo') {
            steps {
                echo 'Code Coverage'
                jacoco()
            }
        }
        stage('Docker build') {
            steps {
                echo 'Docker build'
                echo 'docker build -t brunosilva1988/eureka'
                echo 'docker push brunosilva1988/eureka'
            }
        }
        stage('Deploy') {
            steps {
                echo "docker stack deploy --compose-file docker-compose.yml store"
            }
        }
    }
}