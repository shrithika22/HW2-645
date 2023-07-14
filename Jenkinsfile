pipeline{
	agent any
	environment {
		DOCKERHUB_PASS = "Shrithika"
	}
	stages{
		stage("Generating Build SWE645 student survey"){
			steps{
				script{
					checkout scm
					sh 'rm -rf *.war'
					sh 'jar -cvf homework1.war -C src/main/webapp .'
					sh 'docker login -u shrithika -p ${DOCKERHUB_PASS}'
					sh 'docker build -t shrithika/homework2:0.0.1 .'
				}
			}
		}
		stage("Pushing image to docker"){
			steps{
				script{
					sh 'docker push shrithika/homework2:0.0.1'
				}
			}
		}
		stage("Deploying to rancher"){
			steps{
				script{
				
					sh 'kubectl rollout restart deploy d1 -n 645hw2'
				}
			}
		}
	}
}
