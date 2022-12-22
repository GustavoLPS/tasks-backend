pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh 'apt install -y maven'
                sh 'mvn clean package -DskipTest=true'
            }
        }
    }
}