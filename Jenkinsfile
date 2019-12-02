def app_name = 'gamefication'
def app_funtion = 'backend'

stage 'Checkout'

node {
  checkout scm
}

stage 'Build Image'
node {
   sh "docker build . -t ${app_name}/${app_funtion}"
   sh ' echo $env.BRANCH_NAME'
}

if ($env.BRANCH_NAME == 'master') {
  stage 'Deploying to DEV server'
  node {
    sh "docker-compose up -d "
  }
 }
