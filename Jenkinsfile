pipeline {
    agent any

    stages {
        stage('w/o docker') {
            steps {
                sh '''
                    echo "test"
                    ls -la
                    touch container-no.txt
                '''
            }
        }
        
        stage('with docker') {
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
                    echo "with docker"
                    ls -la
                    touch container-yes.txt
                '''
            }
        }
    }
}
