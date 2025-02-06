// Jenkinsfile (Declarative Pipeline) for integrating Dastardly from Burp Suite

pipeline {
    agent any

    stages {
        stage("Pull Dastardly Docker Image") {
            steps {
                sh 'docker pull public.ecr.aws/portswigger/dastardly:latest'
            }
        }

        stage("Run Dastardly Security Scan") {
            steps {
                cleanWs()
                sh '''
                    docker run --user $(id -u) \
                    -v ${WORKSPACE}:${WORKSPACE}:rw \
                    -e BURP_START_URL=https://ginandjuice.shop/ \
                    -e BURP_REPORT_FILE_PATH=${WORKSPACE}/dastardly-report.xml \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
        }
    }
}
