pipeline {
    agent { label "windows" }
    stages {
        stage('NuGet') {
            steps {
                powershell 'nuget restore'
            }
        }
        stage('Build') {
            powershell "msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=./FolderProfile.pubxml"
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}