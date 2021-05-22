pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh 'jenkins-plugin-cli --plugins docker-compose-build-step:1.0'
                echo 'Downloading...'
                sh 'rm -r JenkinsCommunicatorDeployment'
                sh 'git clone https://github.com/Camillo-commits/JenkinsCommunicatorDeployment.git'
            	sh 'git clone https://github.com/deltachat/deltachat-desktop.git'
                dir("JenkinsCommunicatorDeployment/deltachat"){
                    echo 'Building...'
                    step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml' , option: [$class: 'StartAllServices'], useCustomDockerComposeFile: false])
                }
		dir("deltachat-desktop"){
		    sh 'npm install -verbose'
		    sh 'npm run build'
		}
            }
	    post{
	    	failure{
	 	    echo 'Build Failed'
		}
		success{
		    echo 'Build Passed'
		}
	    }
        }

        stage('Test'){
            steps{
                echo 'Testing...'
                dir("deltachat-desktop"){
		     sh 'npm test'
		}
            }
	    post{
		failure{
		     echo 'Tests Failed'
		}
		success{
		     echo 'Tests Passed'
		}
	    }
        }
	
	stage('Deploy'){
	    steps{
		echo 'Deploying...'
		dir("JenkinsCommunicatorDeployment/deltachat/deployment"){
		     step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml' , option: [$class: 'StartAllServices'], useCustomDockerComposeFile: false])
		}
	    }
	    post{
		failure{
		     echo 'Deployment Failed'
		}
		success{
		     echo 'Deployment Passed'
		}
	    }
	}
    }
}
