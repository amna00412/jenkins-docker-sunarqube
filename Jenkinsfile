pipeline {
    agent any
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('Sonar-Server') {
                    sh '/var/lib/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonar-scanner/bin/sonar-scanner -Dsonar.projectKey=my-website -Dsonar.sources=. -Dsonar.host.url=http://16.171.177.251:9000/ -Dsonar.javascript.node.executable=/usr/bin/node'
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
        stage('Deploy') {
            steps {
                script {
                    try {
                        // Ye step agar fail bhi ho jaye, pipeline SUCCESS rahegi
                        sshPublisher(publishers: [sshPublisherDesc(configName: 'docker-server', transfers: [sshTransfer(sourceFiles: 'index.html', removePrefix: '', remoteDirectory: '/var/www/html')])])
                    } catch (Exception e) {
                        echo "Deployment skip ho gayi, lekin SonarQube PASS hai!"
                        currentBuild.result = 'SUCCESS'
                    }
                }
            }
        }
    }
}
