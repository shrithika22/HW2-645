pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = 'Shrithika'
	}
	stages{
		stage("Building the Student Survey Image"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf homework1.war -C src/main/webapp .'
					sh 'echo ${BUILD_TIMESTAMP}'
					sh 'docker login -u shrithika -p ${DOCKERHUB_PASS}'
					def customImage = docker.build("shrithika/homework2:0.0.1:${BUILD_TIMESTAMP}")
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push shrithika/homework2:0.0.1:${BUILD_TIMESTAMP}'
				}
			}
		}
		
		stage("Deploying to rancher as single pod"){
			steps{
				script{
				
					sh 'kubectl set image deployment/homework2-pipeline homework2-pipeline=shrithika/homework2:0.0.1:${BUILD_TIMESTAMP} -n jenkins-pipeline'
				}
			}
		}
	}
}
