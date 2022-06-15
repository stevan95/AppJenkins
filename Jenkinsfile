pipeline {
   agent any
   environment {
     BRANCHNAME="${env.BRANCH_NAME}"
     COMMIT = sh ( script: 'git rev-parse HEAD', returnStdout: true).trim()
   }
   stages {
      stage('Test') {
        steps {
           echo "Env: $BRANCHNAME $COMMIT"
        }
      }
   }
}
