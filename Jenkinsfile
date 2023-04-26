pipeline {
  agent any

  tools {
      maven 'M2_HOME'
      terraform 'T2_HOME'
        }
  stages {
     stage('checkout'){
       steps {
          git branch: 'main', url: 'https://github.com/snehalatha1/bankingdomain.git'
       }
     }
   

     stage('Package'){
        steps {
            
            sh 'mvn clean package'
        }    
     }  
     stage('publish Reports'){
               steps {
               publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/banking/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])    
                    }
            }

     stage('Docker Image Creation'){
          steps {
                 sh 'docker build -t snehalatha15/bankingdomainapp:latest  .'
                      }
                   }


      stage('Push Image to DockerHub'){
               steps {
                   withCredentials([usernamePassword(credentialsId: 'dh', passwordVariable: 'dhpswd', usernameVariable: 'dhuser')]) {
        	   sh "docker login -u ${env.dhuser} -p ${env.dhpswd}"
                   sh 'docker push snehalatha15/bankingdomainapp:latest'

	            }
                 }
            }
	     
      }
   }
