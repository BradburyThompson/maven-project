pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'docker build . -t tomcatwebapp:${env.BUILD_ID}'
            }
        }
    }
}
