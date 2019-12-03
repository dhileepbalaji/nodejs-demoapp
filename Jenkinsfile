def userInput = true
def didTimeout = false
def app_name = 'gamefication'
def app_funtion = 'backend'
def dev_compose_file = 'mongo-compose.yaml'
def prod_compose_file = 'docker-compose-prod.yaml'

stage 'Checkout Source Code'
// Start Agent 
node {
stage('Checkout code') {
 steps {
    script {
      // Checkout the repository and save the resulting metadata
      def scmVars = checkout([
        $class: 'GitSCM',
        ...
      ])

      // Display the variable using scmVars
      echo "scmVars.GIT_COMMIT"
      echo "${scmVars.GIT_COMMIT}"

      // Displaying the variables saving it as environment variable
      env.GIT_COMMIT = scmVars.GIT_COMMIT
      echo "env.GIT_COMMIT"
      echo "${env.GIT_COMMIT}"
    }

    // Here the metadata is available as environment variable
    ...
  }
}
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
