pipeline{
    agent any
    environment {
        IMAGE_NAME =  "jaiswalakash/java-maven"
        TAG = "v1"
    }
    stages{
        stage('build maven'){
         steps{
             sh 'chmod +x mvnw'
            sh './mvnw clean package'
         }   
        }
        stage('build docker image'){
         steps{
            sh 'docker build -t spring-app1:v1 .'
         }   
        }
        stage('Push Image'){
         steps{
            withCredentials([usernamePassword(
                credentialsId: 'dockerhub',
                usernameVariable: 'USER',
                passwordVariable: 'PASS'
            )])
            {
                sh '''
                echo $PASS | docker login -u $USER --password-stdin
                docker push $IMAGE_NAME:$TAG
                '''
            }
         }   
        }
    }
}
