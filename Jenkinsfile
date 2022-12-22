pipeline {
    agent any
    stages {
        stage ('Build Backend') {
            steps {
                sh 'mvn clean package -DskipTest=true'
            }
        }
        stage ('Unit Tests') {
            steps {
                sh 'mvn test'
            }
        }
        stage ('Sonar Analysis') {
            steps {
                sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://192.168.2.72:9000 -Dsonar.login=sqp_0bc614a06ed4eeb1bb466a36381c284b6dea100a -Dsonar.java.binaries=target"
            }
            // environment {
            //   scannerHome = tool 'SONAR_SCANNER'
            // }
            // steps {
            //     withSonarQubeEnv('SONAR_LOCAL') {
            //         
            //     }
            // }
        }
        stage ('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
    }
}

