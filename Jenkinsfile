def app_name = 'gamefication'
def app_funtion = 'backend'
def compose_file = 'mongo-compose.yaml'

stage 'Checkout'

node {
  checkout scm
}

stage 'Build Image'
node {
   sh "docker build . -t ${app_name}/${app_funtion}"

}

stage 'Deploying to DEV server'
node {
  sh "docker-compose -f ${compose_file} up -d "
  }

