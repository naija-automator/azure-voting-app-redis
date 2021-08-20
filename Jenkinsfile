pipeline {
   agent any
   
   environment {
       DEMO='1.3'
   }   

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            sh(script: 'docker images -a')
            sh(script: """
                cd azure-vote/
                docker images -a
                docker build -t jenkins-pipeline .
                docker images -a 
                cd ..
            """) 
         }
      }
      stage('Checks Build') {
         steps {
            echo "This is build number $BUILD_NUMBER of demo $DEMO"
            sh '''
               echo "Using a multi-line shell step"
               chmod +x test.sh
               ./test.sh
            '''
         }
      }   
   }
}
