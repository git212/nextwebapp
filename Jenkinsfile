pipeline{
    agent any
    environment{
      PATH = "${PATH}:${tool name: 'maven3', type: 'maven'}/bin"
    }
    stages{
        stage('SCM Checkout'){
            steps{
                git branch: "${params['branchName']}",
                    url: 'https://github.com/git212/nextwebapp'
            }
        }

        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }

        stage('Deploy - Dev'){
            steps{
                echo "deploy to dev server "
            }
        }
    }
}