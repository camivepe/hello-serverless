pipeline{
    agent any
    stages{
        stage('build'){
            steps{
                sh 'npm install'
            }
        }
        stage('deploy'){
            steps{
                nodejs(nodeJSInstallationname: 'nodejs') {
                    withAWS(credentials: 'aws-credenntials'){
                        sh 'serverless deploy'
                    }
                }
            }
        }
    }
}