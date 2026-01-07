pipeline {
    agent any
    stages {
        stage('SonarQube Analysis') {
            steps {
                // 'Sonar-Server' wahi naam hai jo aapne Manage Jenkins mein rakha hai
                withSonarQubeEnv('Sonar-Server') {
                    sh '''
                    /var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar-scanner/bin/sonar-scanner \
                    -Dsonar.projectKey=my-website \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=http://16.171.177.251:9000/ \
                    -Dsonar.javascript.node.executable=/usr/bin/node
                    '''
                }
            }
        }
        stage('Quality Gate') {
            steps {
                script {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
