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
    stage('Build Docker test'){
     sh 'docker build -t react-test -f Dockerfile.test --no-cache .'
    }
    stage('Docker test'){
      sh 'docker run --rm react-test'
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }
    stage('Deploy'){
      
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app --no-cache .'
        sh 'docker create -ti --name mimi react-app bash'
        sh 'docker cp mimi:/usr/src/app/build /home/mixy/deploy'
        sh 'docker rm mimi'
        sh 'docker rmi react-app'
        sh 'scp -r /home/mixy/deploy/build mixy@139.162.148.153:/var/www/build'
        sh 'sudo service nginx restart'
      }
    }
  }
  catch (err) {
    throw err
  }
}