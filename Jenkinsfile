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
                zip zipFile: "webapp-${env.GIT_HASH}.zip", archive: false, dir: "bin/app.publish"
                //nexusPublisher nexusInstanceId: 'nx3', nexusRepositoryId: 'files', packages: "webapp-${env.GIT_HASH}.zip"
                nexusArtifactUploader {
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: 'supervm.eastus.cloudapp.azure.com:8081',
                    groupId: 'bhu.webapp',
                    version: '1.0.0',
                    repository: 'files',
                    credentialsId: 'nexus-admin',
                    artifacts: [
                        [artifactId: 'nexus-artifact-uploader',
                        type: 'zip',
                        classifier: 'snapshot',
                        file: "webapp-${env.GIT_HASH}.zip"]
                    ]
                }
            }
        }
    }
    // post {
    //     always {
    //         cleanWs()
    //     }
    // }
}