pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh 'clean package -DskipTest=true'
            }
        }
    }
}