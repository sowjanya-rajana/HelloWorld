pipeline{
    agent any
     tools{
        maven 'Maven'
    }
    stages{
        stage('Git clone'){
            steps{
                git 'https://github.com/sowjanya-rajana/HelloWorld.git'
            }
        }
        
        stage('maven build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('Create Dockerimage'){
            steps{
                sh 'docker build -t gcr.io/nxg-digital/hello-world:latest -f dockerfile .'
            }
        }
        stage('Push Image'){
            steps{
                script{
                     
                    sh 'gcloud auth configure-docker -q '
                    // sh 'docker push gcr.io/${params.DOCKER_REPO}/${params.DOCKER_IMAGE}:${params.DOCKER_TAG} '
                    sh 'docker push gcr.io/nxg-digital/hello-world:latest'
                    
                }
            }
        }
        stage('Remove Image'){
            steps{
                script{
                    echo "Remove docker image"
                    sh 'docker rmi gcr.io/nxg-digital/hello-world:latest '
                    echo "Docker image removed"
                    
                }
            }
        }
        
    }
     post{
    success{
                emailext attachLog: true, body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}", subject: 'Status : $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'sowjanya@nxgsolutions.in'
                 }
    failure{
                echo "failed job!!!"
                emailext attachLog: true, body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}", subject: 'Status : $PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!', to: 'sowjanya@nxgsolutions.in'
              
                }
        }
}
