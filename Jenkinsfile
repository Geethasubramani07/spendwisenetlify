pipeline {
  agent any
  triggers { githubPush() }   // webhook: GitHub -> Jenkins
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Install') {
      steps { sh 'python3 -m venv venv && . venv/bin/activate && pip install -r requirements.txt' }
    }
    stage('Test') {
      steps { sh '. venv/bin/activate && pytest --cov=app --cov-report=xml --cov-report=term-missing' }
    }
    stage('Evaluate metrics') {
      steps { sh '. venv/bin/activate && python scripts/evaluate.py' }
    }
    stage('Package') {
      steps { sh 'docker build -t spendwise:${BUILD_NUMBER} .' }
    }
  }
  post { always { archiveArtifacts artifacts: 'docs/RESULTS.json', allowEmptyArchive: true } }
}
