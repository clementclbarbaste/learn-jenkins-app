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
                withCredentials([string(credentialsId: 'artifactory-npm-token', variable: 'NPM_TOKEN')]) {
                    sh '''
                        cat <<EOF > .npmrc
                        registry=https://artifactory.2b82.aws.cloud.airbus.corp/artifactory/api/npm/npm-airbus-virtual/
                        _authToken=${NPM_TOKEN}
                        always-auth=true
                        strict-ssl=false
                        EOF

                        export PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1
                        npm ci --loglevel verbose
                        rm -f .npmrc
                    '''
                }
            }
        }
    }
}
