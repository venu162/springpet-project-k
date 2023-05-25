pipeline {
    agent any
     parameters { string(name: 'continuous-download','continuous-build',description: 'stages_names')
     choice(name: 'BRANCH', choices: ['master'], description: 'branch_name')
      }
    triggers {
      pollSCM ('* * * * *')
    }
    stages{
        stage('continuous-download'){
            steps{
                echo "hello: ${params.name}"
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
    }
}