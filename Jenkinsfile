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
               sh 'dotnet clean '
            }
         }
         
        stage('Build'){
           steps{
               sh 'dotnet build '
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