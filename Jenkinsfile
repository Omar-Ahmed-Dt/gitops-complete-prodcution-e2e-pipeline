   pipeline{
    agent{
        label "jenkins-agent"
    }
    environment{
        APP_NAME = "complete-prodcution-e2e-pipeline"
    }
    stages{
        stage("Cleanup Workspace"){
            steps {
                cleanWs()
            }

        }
        stage("Checkout from SCM"){
            steps {
                git 'https://github.com/Omar-Ahmed-Dt/gitops-complete-prodcution-e2e-pipeline.git'
            }

        }

        stage("Update the deployment Tags"){
            steps{
                sh """
                    cat deployment.yaml
                    sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                    cat deployment.yaml
                """
            }

        } 

        stage("Push the changed deployment file to Git"){
            steps{
                sh """
                    git config --global user.name "Omar-Ahmed-Dt"
                    git config --global user.email "omarahmed9113@gmail.com"
                    git add deployment.yaml
                    git commit -m "Updated Deployment Manifest"
                """
                sh "git push https://github.com/Omar-Ahmed-Dt/gitops-complete-prodcution-e2e-pipeline.git main"
            }


        }
    }
   }
