pipeline {
    agent any

    stages {   
        stage('Build') {
            agent{
                docker {
                    image 'docker-airbus-virtual.artifactory.2b82.aws.cloud.airbus.corp/library/node:26-alpine'
                    registryUrl 'https://docker-airbus-virtual.artifactory.2b82.aws.cloud.airbus.corp'
                    registryCredentialsId 'ArtifactoryToken'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    echo "Starting Build"
                    ls -la
                    node --version
                    npm --version
                    npm ci
                    npm run build
                '''
            }
        }
    }
}
