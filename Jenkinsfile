pipeline{

    agent {label 'slave1'}

    stages {
        
        stage("cloning git repository"){
            steps{
                git branch: 'develop', credentialsId: 'github_id', url: 'https://github.com/rheanegi24/BackendLx.git'
            }
        }    
        stage("build"){
            steps{
               sh "mvn clean install"
            }    
        }
        
        stage('Building image') {
    steps{
        script {
            dockerImage = docker.build "packersmovers:1.0.0"
        }
    }
}
        
    stage('Stop and delete the running container') {
         steps{  
             catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE'){
                    sh "docker stop springboot"
                    sh "docker rm springboot"
             }    
        }
    }  
    stage('RUN IMAGE') {
         steps{  
            sh "docker run -d --name springboot -p 8081:8081  packersmovers:1.0.0"
            }
         }    
    }
}
