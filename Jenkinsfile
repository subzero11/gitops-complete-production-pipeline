pipeline{
    agent{
        label 'jenkins-agent'
    }
    environment{
        APP_NAME = "gitops-complete-production-pipeline"
    }

    stages{

        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }
        stage("Checkout from SCM"){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/subzero11/gitops-complete-production-pipeline'
            }
        }
        stage("Update the Deployment Tags"){
            steps{
                sh '''
                    cat deployment.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml                 
                   '''
            }
        }
        stage("Push the Deployment file to Git"){
            steps{
                sh '''
                    git config --global user.name 'tkhan'                
                    git config --global user.email 'nyguy@hotmail.com
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"               
                   '''
                   withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: "Default")]){
                    sh "git push https://github.com/subzero11/gitops-complete-production-pipeline main"
                   }
            }
        }    
    }
}
