library identifier: 'SharedLibrary@master', retriever: modernSCM(
  [$class: 'GitSCMSource', remote: 'https://github.com/stevan95/SharedLibrary.git'])


pipeline {
   agent any
   environment {
     BRANCHNAME="${env.BRANCH_NAME}"
     COMMIT = sh ( script: 'git rev-parse HEAD | cut -c1-8', returnStdout: true).trim()
     APP_NAME="mongo"
   }
   stages {
      stage('Build') {
        steps {
           script {
             build()
           }
        }
      }
   }
}
