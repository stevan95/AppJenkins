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
               docker run --name $APP_NAME -d $IMAGE
               
               if [ "$(docker ps -q -f name=$APP_NAME)" ]; then
                  echo "Container is running successfuly"
                  docker rm -f $APP_NAME
               else
                  echo "Failed to run container in background"
                  docker rm -f $APP_NAME
                  exit 1
               fi

               '''
            }
         }
      }
   }
}
