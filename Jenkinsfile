pipeline {
    agent any
     parameters {
     choice(name: 'BRANCH', choices: ['master'], description: 'branch_name')
      }
    triggers {
      pollSCM ('* * * * *')
    }
    stages{
        stage('continuous-download'){
            steps{
                git 'https://github.com/spring-projects/spring-petclinic.git'
                echo "choice: ${params.BRANCH}"
            }
        }
       stage('continuous-build'){
            steps{
              sh 'sudo apt install openjdk-17-jdk -y'
              sh 'sudo apt install maven -y'
              sh 'mvn package'
            }
        }
        stage('SonarQube analysis') {
           //    def scannerHome = tool 'SonarScanner 4.0';
            steps{
                withSonarQubeEnv('sonarqube-8.3'){
                   // If you have configured more than one global server connection, you can specify its name
                   //  sh "${scannerHome}/bin/sonar-scanner"
                   sh "mvn sonar:sonar"
                }
            }
        }
    }
}