pipeline {
	agent any
	triggers{
		pollSCM '* * * * *'
	}
	stages{
		stage('TEST'){
			steps{
				bat 'mvn test'
			}
		}
		stage('BUILD'){
			steps{
				bat 'mvn clean package'
			}
		}
		stage('DEPLOY TO CLOUDHUB'){
			environment{
				ANYPOINT_CREDENTIALS = credentials('AnypointPlatform')
			}
			steps{
				bat 'mvn deploy -DmuleDeploy -DskipTests -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2 -Denvironment=Sandbox'
			}
		}
	}
}
