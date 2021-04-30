pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                sh 'jenkins-plugin-cli --plugins docker-compose-build-step:1.0'
                echo 'Downloading...'
                sh 'rm -r JenkinsCommunicatorDeployment'
                sh 'git clone https://github.com/Camillo-commits/JenkinsCommunicatorDeployment.git'
            
                dir("JenkinsCommunicatorDeployment/deltachat"){
                    echo 'Building...'
                    step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml' , option: [$class: 'StartAllServices'], useCustomDockerComposeFile: false])
                }
            }
        }
        stage('Test'){
            steps{
                echo 'Testing...'
                
                dir("JenkinsCommunicatorDeployment/tests"){
                    //sh 'make check || true'
                    step([$class: 'DockerComposeBuilder', dockerComposeFile: 'docker-compose.yml' , option: [$class: 'StartAllServices'], useCustomDockerComposeFile: false])
                }
            }
        }
    }
    post {
        failure{
           echo 'Tests Failed'
        }
        success{
            echo 'Tests Passed'
        }
    }
}
