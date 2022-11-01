pipeline {
    agent { label "windows" }
    stages {
        stage('Descargar dependencias') {
            steps {
                powershell 'nuget restore'
            }
        }
    }    
}