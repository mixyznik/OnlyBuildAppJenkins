node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Deploy'){
      
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app --no-cache .'
        sh 'docker create -ti --name mimi react-app bash'
        sh 'docker cp mimi:/usr/src/app/build /deploy'
        sh 'docker rm mimi'
        sh 'docker rmi react-app'
      }
    }
  }
  catch (err) {
    throw err
  }
}