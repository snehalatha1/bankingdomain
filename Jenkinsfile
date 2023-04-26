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
                 sh 'docker build -t snehalatha15/finance:latest  .'
                      }
                   }


      stage('Push Image to DockerHub'){
               steps {
                   withCredentials([string(credentialsId: 'dock', variable: 'dhp')]){
			   sh 'docker login -u snehalatha15 -p "echo ${dhp}"'
		   }
                   sh 'docker push snehalatha15/finance:latest'

	            }
                 }
            }
	     
      }
