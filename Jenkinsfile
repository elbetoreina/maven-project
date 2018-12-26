

pipeline{

    agent any

    

    stages{
        stage('Build'){
            steps{
                sh '/home/areina/apache-maven-3.5.4/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }                
            }
        }
        stage('Deploy to Staging'){
            steps {
                build job: 'deploy-to-staging'
            }
        }
    }
}