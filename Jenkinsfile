pipeline {
    agent { label "windows" }
    stages {
        stage('NuGet') {
            steps {
                powershell 'nuget restore'
            }
        }
    }
}