pipeline {
    agent any
    stages {
        stage('SonarQube Analysis') {
            steps {
                // Yahan "Sonar-Server" wahi naam hai jo aapne Jenkins settings mein rakha hai
                withSonarQubeEnv('Sonar-Server') {
                    sh 'echo "Running SonarScan..." '
                    // Agar aapka scanner command hai toh wo yahan aayega
                }
            }
        }
        stage('SonarQube Quality Gate') {
            steps {
                script {
                    timeout(time: 5, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}
