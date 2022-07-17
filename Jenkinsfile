pipeline {
   agent { label 'agent-1' }
   environment {
     BRANCHNAME="${env.BRANCH_NAME}"
     COMMIT = sh ( script: 'git rev-parse HEAD | cut -c1-8', returnStdout: true).trim()
     APP_NAME="mongo"
     IMAGE="${BRANCH_NAME}:${COMMIT}"
   }
   stages {
      stage('Build') {
        steps {
           sh 'docker build -t $IMAGE .'
        }
      }

      stage('Test') {
         steps {
            script {
               sh '''
                  docker run -d $IMAGE
                  STATUS=`docker ps | grep mongo | awk ' { print $1 } '`
                  if [-z "$STATUS"];
                     echo "Test is failed."
                  else
                     echo "Test is successful."
                  fi

                  docker rm -f $STATUS
               '''
            }
         }
      }
   }
}
