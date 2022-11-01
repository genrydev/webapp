pipeline {
    agent { label "windows" }
    stages {
        stage('NuGet') {
            steps {
                powershell 'nuget restore'
            }
        }
        stage('Build') {
            steps {
                powershell 'msbuild /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=./FolderProfile.pubxml'
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}