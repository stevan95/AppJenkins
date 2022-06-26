pipeline {
   agent any
   environment {
     BRANCHNAME="${env.BRANCH_NAME}"
     COMMIT = sh ( script: 'git rev-parse HEAD | cut -c1-8', returnStdout: true).trim()
   }
   stages {
      stage('Build') {
        steps {
           sh 'docker build -t ${BRANCH_NAME}:${COMMIT} .'
        }
      }
   }
}
