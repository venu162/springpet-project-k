pipeline {
    agent any
    stages{
        stage('continuous-download'){
            steps{
                git 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }
       stage('continuous-build'){
            steps{
              sh 'sudo apt install openjdk-17-jdk -y'
              sh 'sudo apt install maven -y'
              sh 'mvn package'
            }
        }
        stage('continuous-deplyoment'){
            steps{
              archiveArtifacts artifacts: '**\*.war'
            }
        }
    }
}