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
            sh 'sudo apt install maven git -y'
            sh 'clean package'
        }
       }
    }
}