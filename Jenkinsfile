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
        stage('artifactory-config'){
            steps{
               rtServer(
                   id: "qtdevo",
                   url: "https://qtdevo.jfrog.io/",
                   credentialsId: "JFROG_ADMIN_ID"
                )
                rtMavenDeployer(
                    id: "MAVEN_DEPLOYER",
                    serverId: "qtdevo",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )
            }
        }
    }
}