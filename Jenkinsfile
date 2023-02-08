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
     sh 'docker build -t goapp-test -f Dockerfile --no-cache .'
    }
    stage('Docker test'){
      sh 'docker run --rm goapp-test'
    }
    stage('Clean Docker test'){
      sh 'docker rmi goapp-test'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'Ali'){
        sh 'sudo docker build -t react-app --no-cache .'
        sh 'sudo docker tag react-app localhost:80/react-app'
        sh 'sudo docker push localhost:80/react-app'
        sh 'sudo docker rmi -f react-app localhost:80/react-app'
      }
    }
  }
  catch (err) {
    throw err
  }
}
