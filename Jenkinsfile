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
    
 stage("Install Project Dependencies"){

        steps{
            sh 'composer install'
        }
    } 
       

    // Docker build and push to docker-hub //

    stage(' Docker Build and Push '){
        steps{
            echo 'Building Started'
            script{
                    docker.withRegistry('', 'docker-creds'){
                    def customerimage = docker .build('https://hub.docker.com/repository/docker/chetancc023/magento:tagname')
                    customerImage.push('${currentBuild.id}')   

                }


            }


        }
    }
}
}
