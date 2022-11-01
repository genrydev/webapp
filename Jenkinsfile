pipeline {
    agent { label "windows" }
    environment {
        GIT_HASH = GIT_COMMIT.take(8)
    }
    stages {
        stage('NuGet') {
            steps {
                //powershell "C:\\tools\\nuget.exe restore"
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
                //echo "${env.WORKSPACE}"
                //echo "${env.GIT_HASH}"
                zip zipFile: "webapp.zip-${env.GIT_HASH}", archive: false, dir: "bin/app.publish"
            }
        }
    }
    // post {
    //     always {
    //         cleanWs()
    //     }
    // }
}