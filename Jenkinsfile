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
            }
        }
        stage('artifactory-config'){
            steps{
               rtMavenDeployer(
                 id: "qtdevo",
                 serverId: "qt_maven",
                 releaseRepo: "libs-release-local",
                 snapshotRepo: "libs-snapshot-local"
                )
            }
        } 
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: "maven", // Tool name from Jenkins configuration
                    pom: "pom.xml",
                    goals: "package",
                    deployerId: "qtdevo"
                )
            }
        }   
    }
}