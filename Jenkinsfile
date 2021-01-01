pipeline {
	agent any
	triggers{
		pollSCM '* * * * *'
	}
	stages('TEST'){
		steps{
			bat 'mvn test'
		}
	}
	stages('BUILD'){
		steps{
			bat 'mvn clean package'
		}
	}
	stages('DEPLOY ARTIFACT TO ARTIFACTORY'){
		steps{
			bat 'mvn deploy'
		}
	}
	stages('DEPLOY TO CLOUDHUB'){
		environment{
			ANYPOINT_CREDENTIALS = credentials(AnypointPlatform)
		}
		steps{
			bat 'mvn deploy -DmuleDeploy -Dusername=${ANYPOINT_CREDENTIALS_USR} -Dpassword=${ANYPOINT_CREDENTIALS_PSW} -DworkerType=Micro -Dworkers=1 -Dregion=us-west-2 -Denvironment=Sandbox'
		}
	}
}
