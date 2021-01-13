pipeline {
    agent any
    environment {
        registry = "tadeuuuuu/infra-developer"
    }
    
    stages {
        
        stage('Test') {
        agent {
          dockerfile {
            filename "productpage/Dockerfile"
          }}
          steps {
            sh 'echo Test'
          }
        }
        
        stage('Build') {
          steps { 
            sh "pwd"
            sh "ls -la" 
            sh "cd reviews/" 
            sh "pwd"
            sh "ls -la" 
            sh "docker run --rm -u root -v `pwd`:/home/gradle/project -w /home/gradle/project gradle:4.8.1 gradle clean build"
            sh "cd .." 
            sh "docker build --file=reviews/reviews-wlpcfg/Dockerfile --tag $registry:reviews-$BUILD_NUMBER reviews/reviews-wlpcfg"
          } 
        }

        stage('Publish') {
            steps {
                sh 'echo Publish'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'echo Deploy'
            }
        }
    }
}

