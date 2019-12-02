def app_name = 'gamefication'
def app_funtion = 'backend'

def getGitBranchName() {
    return scm.branches[0].name
}

stage 'Checkout'

node {
  checkout scm
}

stage 'Build Image'
node {
   sh "docker build . -t ${app_name}/${app_funtion}"

}

if ( getGitBranchName == 'master') {
  stage 'Deploying to DEV server'
  node {
    sh "docker-compose up -d "
  }
 }
