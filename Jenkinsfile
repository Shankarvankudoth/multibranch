pipeline { 
  
   agent any

   stages {
   
     stage('Install Dependencies') { 
        steps { 
           sh 'npm ci' 
        }
     }
     
     stage('Test') { 
        steps { 
           sh 'echo "testing application..."'
        }
      }

         stage("Deploy npm cloud application") { 
         steps { 
           sh 'echo "deploying application..."'
         }

     }
  
   	}

   }
