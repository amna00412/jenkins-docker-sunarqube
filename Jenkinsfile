stage('SonarQube Quality Gate') {
    steps {
        script {
            def qg = waitForQualityGate()
            if (qg.status != 'OK') {
                echo "Quality gate failed: ${qg.status}"
            }
        }
    }
}
