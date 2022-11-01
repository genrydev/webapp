pipeline {
    agent { label "windows" }
    stages {
        stage('Descargar dependencias') {
            steps {
                powershell 'nuget restore'
            }
        }
        stage('Build') {
            steps {
                powershell 'msbuild /verbosity:quiet /p:Configuration=Release /p:DeployOnBuild=true /p:PublishProfile=./FolderProfile.pubxml'
            }
        }
    }    
}