pipeline {
    agent {
            label "dotnet"
        }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        
        stage('Clean'){
           steps{
               sh 'dotnet clean  --configuration Release'
            }
         }
         stage("Get dir size") {
            script {
                DIR_SIZE = sh(returnStdout: true, script: 'ls -la /var | grep jenkins_home | cut -d " " -f5')
            }
            echo "dir size = ${DIR_SIZE}"
            }
        stage('Build'){
           steps{
               sh 'dotnet build --configuration Release --no-restore'
            }
         }
        stage('Test: Unit Test'){
           steps {
                sh 'dotnet test TestProject1/TestProject1.csproj --configuration Release --no-restore'
             }
          }
        stage('Publish'){
             steps{
               sh 'dotnet publish --configuration Release --no-restore'
             }
        }
        stage('Deploy'){
             steps{
               sh '''for pid in $(lsof -t -i:9090); do
                       kill -9 $pid
               done'''
             
             }
        }
    }
}