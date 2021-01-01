pipeline{
agent any
triggers{ cron('* * * * *') }
stages{
stage('JOKE'){
steps{
sh 'mvn clean'
bat 'mvn clean install'}
}}
}
