pipeline{
    agent {
        label "agent-01" 
    }
    tools {
        maven "mavn-3-5-4"
        jdk "JDK-11"    
    }
    environment {
        DOCKER_USERNAME = credentials('docker-username')
        DOCKER_PASSWORD = credentials('docker-password')
        DEPI_ROUND = "R4"
    }
    stages {
        stage("Build Application") {
                steps {
                    sh "mvn package install -DskipTests"
                    sh "echo ${DEPI_ROUND}"
                }
            }
          stage("Test Application") {
                steps {
                    sh "mvn test"
                }
            }
            stage("Build image") {
                steps {
                    sh "docker build -t ${DOCKER_USERNAME}/depi-jenkins:v${BUILD_NUMBER} ."
                }
            }
            stage("Push image") {
                steps {
                    sh 'echo ${DOCKER_PASSWORD} | docker login -u ${DOCKER_USERNAME} --password-stdin'
                    sh 'docker push ${DOCKER_USERNAME}/depi-jenkins:v${BUILD_NUMBER}'
                }
            }
    }
}