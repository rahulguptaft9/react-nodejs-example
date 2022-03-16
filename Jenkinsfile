pipeline {
    
	  agent any
  tools {nodejs "node"}

	environment{
	registry="mrchelsea/docker-image"
	registryCredential='dockerhub'
	dockerImage=''
	}
    
    //def registry = 'mrchelsea/testing-docker'
    //def registryCredential = 'dockerhub'
	stages{
	stage('Git') {
		steps{
		git 'https://github.com/rahulguptaft9/react-nodejs-example'
		}	
	}
	stage('Build') {
		steps{
		sh 'npm install'
		}	
	}
	stage('Test') {
		steps{
		sh 'npm test'
		}
	}
	stage('Building image') {
		steps{
			script{
			 	dockerImage=docker.build registry	
			}
		}
	}
	stage('Registring image') {
		steps{
			script{
				docker.withRegistry('',registryCredential){
				dockerImage.push()
				}
			}
		}
	}
	}
    
}
