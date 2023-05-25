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
              archiveArtifacts artifacts: '**\*.war', followSymlinks: false
            }
        }
        stage('continuous-testing'){
            steps{
                copyArtifacts fingerprintArtifacts: true, projectName: 'qtdevops', selector: lastSuccessful(), target: '/var/lib/jenkins/workspace/qtdevops/target/spring-petclinic-3.0.0-SNAPSHOT.jar'
            }
        }
    }
}