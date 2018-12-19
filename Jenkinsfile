

pipeline{

    agent any

    tools {
        jdk 'jdk-1.8.0_131'
        maven 'maven-3.5.4'
    }

    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }                
            }
        }
    }
}