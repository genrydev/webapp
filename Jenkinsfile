pipeline {
    agent { label "windows" }
    environment {
        GIT_HASH = GIT_COMMIT.take(8)
    }
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
        stage ('Upload Artifact'){
            steps {
                //echo "${env.WORKSPACE}"
                echo "${env.GIT_HASH}"                
            }
        }
    }    
}