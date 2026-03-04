pipeline{
    agent {
        label "agent-01" 
    }
    tools {
        maven "mavn-3-5-4"
        jdk "JDK-11"    
    }
    stages {
        stage("Build Application") {
                steps {
                    sh "mvn package install -DskipTests"
                }
            }
          stage("Test Application") {
                steps {
                    sh "mvn test"
                }
            }
            stage("Build image") {
                steps {
                    sh" docker build -t java-app:${BUILD_NUMBER} ."
                }
            }
    }
}