pipeline {
  agent any
  triggers { pollSCM('* * * * *') }
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Validate') {
      steps { sh 'kubectl apply --dry-run=client -f k8s/app.yaml' }
    }
    stage('Deploy') {
      steps { sh 'kubectl apply -f k8s/app.yaml' }
    }
    stage('Verify') {
      steps { sh 'kubectl -n food-delivery rollout status deploy/restaurant-service --timeout=120s' }
    }
  }
}
