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
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp -i C:/Users/Bili/Desktop/Fullstack/CICD/tomcat-demo2.pem **/target/*.war ec2-user@${params.tomcat_dev}:/home/ec2-user/apache-tomcat-9.0.13/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -i C:/Users/Bili/Desktop/Fullstack/CICD/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/home/ec2-user/apache-tomcat-9.0.13/webapps"
                    }
                }
            }
        }
    }
}