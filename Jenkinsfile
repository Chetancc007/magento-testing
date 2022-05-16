pipeline {

agent any

options {

    skipDefaultCheckout()
    disableConcurrentBuilds()
    disableResume()
    }
    
 environment {
    imagename = "chetancc023/magento"
    dockerImage = ''
    //scannerHome = tool 'SonarQubeScanner'
  }   
parameters {

    string(name: 'imagename', defaultValue: '1.0', description: 'tagname')
    string(name: 'version', defaultValue: '1.0', description: 'tagname')
}

stages{

    // checkout stage //
    stage('checkout from GIT'){
        steps{
            checkout scm
        }
    }

    // Docker build and push to docker-hub //

    stage(' Docker Build and Push '){
        steps{
            echo 'Building Started'
            script{
                dockerImage = docker.build imagename
                docker.withRegistry('', 'docker-creds') {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')    

                }


            }


        }
    }
