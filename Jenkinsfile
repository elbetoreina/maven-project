pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '54.212.234.202', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.219.188.123', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh '/home/areina/apache-maven-3.5.4/bin/mvn clean package'
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
                        sh "scp -v -o StrictHostKeyChecking=no /etc/ssh/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp -v -o StrictHostKeyChecking=no /etc/ssh/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}