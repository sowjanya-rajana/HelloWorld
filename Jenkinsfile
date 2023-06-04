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
                sh 'docker build -t gcr.io/nxg-digital/springboot:latest -f dockerfile .'
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
