pipeline {
    agent any

    parameters {
        string(name: 'tomcat_dev', defaultValue: '3.120.235.62', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: '52.28.177.30', description: 'Production Server')
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages{
        stage('Build'){
                steps {
                    bat 'mvn clean package'
                }
                post {
                    success {
                        echo 'Now Archiving...'
                        archiveArtifacts artifacts: '**/target/*.war'
                    }
                }
            }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "pscp -i C:/Users/Bili/Desktop/Fullstack/CICD/tomcat-demo2.ppk **/target/*.war ec2-user@${params.tomcat_dev}:/home/ec2-user/apache-tomcat-9.0.13/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "winscp -i C:/Users/Bili/Desktop/Fullstack/CICD/tomcat-demo.ppk **/target/*.war ec2-user@${params.tomcat_prod}:/home/ec2-user/apache-tomcat-9.0.13/webapps"
                    }
                }
            }
        }
    }
}