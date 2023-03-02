pipeline {

    agent any
    parameters {
        string(name: 'ENV_TAG', defaultValue: 'dev')
    }
    environment {
           APP_NAME = "mifos-ui"
           IMAGE_BASE_NAME = "${CI_REGISTRY}/${APP_NAME}"           
    }

    stages {
        
        stage('Docker Build & Push Image') {
            when {
                anyOf {
                    branch "master"; branch "dev"
                }
            }
            steps {
              script {

                if(env.BRANCH_NAME == "master"){
                    env.ENV_TAG = "prod"
                }

                 sh '''
                    IMAGE_TAG="${ENV_TAG}_$(date +%Y-%m-%d-%H-%M)"
                    IMAGE_NAME="${IMAGE_BASE_NAME}:${IMAGE_TAG}"
                    docker build  -f Dockerfile -t $IMAGE_NAME .
                    docker push $IMAGE_NAME
                '''
              }
            }
        }
    }
}
