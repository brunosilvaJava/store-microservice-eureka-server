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
        stage('Docker build') {
            steps {
                sh 'docker build -t brunosilva1988/eureka'
                sh 'docker push brunosilva1988/eureka'
            }
        }
        stage('Deploy') {
            steps {
                sh "docker stack deploy --compose-file docker-compose.yml store"
            }
        }
    }
}