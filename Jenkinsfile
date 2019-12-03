def userInput = true
def didTimeout = false
def dev_compose_file = 'docker-compose-dev.yaml'
def prod_compose_file = 'docker-compose-prod.yaml'

node {

stage 'Clean WorkSpace'
       cleanWs()

stage 'Checkout code'
      // Checkout the repository and save the resulting metadata
      final scmVars = checkout(scm)
      env.TAG = "${scmVars.GIT_COMMIT}"
      echo "scmVars: ${TAG}"


stage 'Build Image'
      
      sh "docker build . -t ${APP_NAME}/${APP_TYPE}:${TAG}"

stage 'dev'
      
      env.RELEASE_ENVIRONMENT = "dev"
      env.STAGE_NAME = "dev"
      sh "docker-compose -f ${dev_compose_file} up -d "
}

// Kill Agent
stage 'Approval'
// Input Step
timeout(time: 15, unit: "MINUTES") {
    input id: 'Deploy', submitter: 'admin', message: 'Do you want to approve the deploy in production?', ok: 'Yes'
}
// Start Agent Again
node {
stage 'prod'
      env.RELEASE_ENVIRONMENT = "dev"
      sh "docker-compose -f ${prod_compose_file} up -d "
  
}
