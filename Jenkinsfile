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
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId:'herokucredentials', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
  
}
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app --build-arg SMB_USER=USERNAME --build-arg SMB_PASS=PASSWORD --no-cache .'
        sh 'docker rmi react-app'
      }
    }
  }
  catch (err) {
    throw err
  }
}