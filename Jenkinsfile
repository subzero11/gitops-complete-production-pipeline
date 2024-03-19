pipeline{
    agent{
        label "jenkins-agent"
    }
    environment{
	    APP_NAME = "complete-production-pipeline"
    }
    stages{
        stage('Clean Workspace'){
            steps{
                cleanWs()
            }
            }
        stage('Checkout from SCM'){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/subzero11/gitops-complete-production-pipeline'
            }
        }
        stage('Update the Deployment Tags'){
            steps{
                sh """
                cat deployment.yaml
                sed -i 's/${APP_NAME}.*/${APP_NAME}=${IMAGE_TAG}/g' deployment.yaml
                cat deployment.yaml
                """
            }
        }  
	    
    }
}
