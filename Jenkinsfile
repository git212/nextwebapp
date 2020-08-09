pipeline{
    agent any
    environment{
       PATH = "${PATH}:${tool name: 'maven3', type: 'maven'}/bin"
    }
    stages{
        stage('SCM Checkout'){
            steps{
                git url: 'https://github.com/git212/nextwebapp',
                branch: 'master',
                credentialsId: 'github'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh 'mvn clean package'
            }
        }

        stage('Deploy Dev'){
            steps{
                sshagent(['tomcat-dev']) {
                    // stop tomcat
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.34.81 /opt/tomcat8/bin/shutdown.sh"
                    // copy war file to remote tomcat
                    sh "scp target/nextwebapp.war ec2-user@172.31.34.81:/opt/tomcat8/webapp/"
                     // start tomcat
                    sh "ssh ec2-user@172.31.34.81 /opt/tomcat8/bin/startup.sh"
                }
            }
        }
    }
}