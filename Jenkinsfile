pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	
	agent any
	
    stages{
        stage('Checkout on master'){
			agent {
				label 'master'
			}
            steps{
		        echo 'cloning...'
                 git 'https://github.com/mercykola/JUNECLASSPRO1.git'
              }
          }
         
		stage('Compile on slave1') {
			agent {
				label 'slave1'
			}
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	          }
          }
		
          stage('CodeReview on slave2'){
			  agent {
				label 'slave2'
			}
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
		stage('UnitTEST on slave1') {
			agent {
				label 'slave1'
			}
              steps{
                  echo 'Testing..'
                  sh 'mvn test'
			  }
          	  post {
				  success{
					  junit 'target/surefire-reports/*.xml'
				  }
			  }
		}



          
          stage('Package on master'){
			  agent {
				label 'maaster'
			}
              steps{
				  echo 'Packaging...'
                  sh 'mvn package'
              }
          }
      }
}
