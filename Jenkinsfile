pipeline{
    agent any
    stages{

        stage('build sin test'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs') {
                    sh 'npm install'
                    sh 'npm rebuild'
                    sh 'npm run build --skip-test --if-present'
                    // stash name: "ws", include: "**"
                }
            }
        }

        stage('unitTest'){
            steps{
                //unstash "ws"
                nodejs(nodeJSInstallationName: 'nodejs') {
                    sh 'npm run test:coverage && cp coverage/lcov.info icov.info || echo "Code coverage failed"'
                    archiveArtifacts(artifacts: 'coverage/**', onlyIfSuccessful: true)
                }
            }
        }
        
        stage('deploy'){
            steps{
                nodejs(nodeJSInstallationName: 'nodejs') {
                    withAWS(credentials: 'aws-credenntials'){
                        sh 'serverless deploy'
                    }
                }
            }
        }

    }
}