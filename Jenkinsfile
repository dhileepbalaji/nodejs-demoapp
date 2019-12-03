def userInput = true
def didTimeout = false
def app_name = 'gamefication'
def app_funtion = 'backend'
def dev_compose_file = 'mongo-compose.yaml'
def prod_compose_file = 'docker-compose-prod.yaml'

stage 'Checkout Source Code'
// Start Agent 
node {
  checkout scm

stage 'Build Image'

   sh "docker build . -t ${app_name}/${app_funtion}"

stage 'dev'
  
  sh "printenv | sort"
  sh "docker-compose -f ${dev_compose_file} up -d "
}

// Kill Agent

// Input Step
timeout(time: 15, unit: "MINUTES") {
    input message: 'Do you want to approve the deploy in production?', ok: 'Yes'
}
// Start Agent Again
node {
stage 'prod'

  sh "docker-compose -f ${prod_compose_file} up -d "
  
}
