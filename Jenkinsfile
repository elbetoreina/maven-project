pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh '/home/areina/apache-maven-3.5.4/bin/mvn clean package'
                sh "docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
        }
    }
}