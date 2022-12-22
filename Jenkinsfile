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
            environment {
              scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL') {
                    sh "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://192.168.2.72:9000 -Dsonar.login=sqp_0bc614a06ed4eeb1bb466a36381c284b6dea100a -Dsonar.java.binaries=target"
                }
            }
        }
        stage ('Quality Gate') {
            steps {
                sleep(10)
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate(webhookSecretId: 'squ_3ba5c765349581ddce4e1947d407691e3f4de1ff') abortPipeline: true
                }
            }
        }
    }
}

