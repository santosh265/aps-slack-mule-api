pipeline {
	agent any
	trigger{
		pollSCM '* * * * *'
	}
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
	stage('DEPLOY ARTIFACT TO ARTIFACTORY'){
		steps{
			bat 'mvn deploy'
		}
	}
	stage('DEPLOY TO CLOUDHUB'){
		steps{
			bat 'mvn deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2 -Denvironment=Sandbox'
		}
	}
}
