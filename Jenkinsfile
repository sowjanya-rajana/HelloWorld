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
                sh 'docker build -t gcr.io/nxg-digital/springboot:latest .'
            }
        }
        
    }
}
