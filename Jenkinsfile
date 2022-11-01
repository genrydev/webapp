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
        stage ('Upload Artifact'){
            steps {
                echo "${env.WORKSPACE}"
                //zip zipFile: 'webapp.zip', archive: false, dir: './archive'
            }
        }
    }
    // post {
    //     always {
    //         cleanWs()
    //     }
    // }
}