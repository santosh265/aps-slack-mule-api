pipeline{
agent any
triggers {
        pollSCM '* * * * *'
    }
stages{
stage('JOKE'){
steps{
sh 'mvn clean'
bat 'mvn clean install'}
}}
}
