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

    stage(' Docker Build and Push To Docker-Hub '){
        steps{
            echo 'Building Started'
            script{
                dockerImage = docker.build imagename
                docker.withRegistry('', 'docker-creds') {
                dockerImage.push("latest")
                dockerImage.push('latest')    

                }


            }


        }
    }
    // Pulling docker images from hub and deploying using docker-compose method//
   stage('Deploy'){
       
       steps{
                    sh """
                        cd ~/magento-test
                        docker-compose -f docker-compose pull
                        docker-compose -f docker-compose up -d
                    """
             
       }
   }
    
    
}
}
