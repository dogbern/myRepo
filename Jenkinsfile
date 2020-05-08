pipeline {
	agent any
	stages {
		stage ("Lint HTML"){
			steps {
				sh 'tidy -q -e *.html'
			}
		}
		stage ('Upload to AWS') {
			steps {
				sh 'echo "Hello World with AWS creds"'
				withAWS(region:'us-west-2',credentials:'aws-static'){
					s3Upload(file:'index.html', bucket:'static-jerkins-pipeline')
				}
			}
		}
		stage ('Web Page Status'){
			steps {
				sh 'curl http://static-jerkins-pipeline.s3-website-us-west-2.amazonaws.com -s -f -o /dev/null || echo "Website Down!"'
			}
		}
	}
}