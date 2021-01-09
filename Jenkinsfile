pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '54.226.106.120', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '3.83.191.89', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                echo 'fake mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    echo 'fake archive'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}
