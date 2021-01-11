pipeline {
    agent any
    environment {
        ENV_NAME = "${env.BRANCH_NAME == "develop" ? "Sandbox" : "Production"}"
        APP_TAG = "${env.ENV_NAME == "Sandbox" ? "dev" : "prod"}"
        APP_NAME = "aps-slack-mule-api-${APP_TAG}"
    }
    triggers{
        githubPush()
    }
    stages{
        stage('TEST'){
            steps{
            	sh 'printenv'
                bat 'mvn test'
            }
        }
        stage('BUILD'){
            steps{
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('PUBLISH ARTIFACT TO JFROG'){
        	steps{
        		bat 'mvn -X deploy'
        	}
        }
        stage('DEPLOY TO CLOUDHUB'){
            environment{
                ANYPOINT_CREDENTIALS = credentials('AnypointPlatform')
            }
            steps{
                bat 'mvn deploy -DmuleDeploy -DskipTests -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DapplicationName=${APP_NAME} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2 -Denvironment=${ENV_NAME}'
            }
        }
    }
}
