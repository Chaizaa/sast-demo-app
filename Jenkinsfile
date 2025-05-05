pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/Chaizaa/sast-demo-app.git', branch: 'master'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '''
          python3 -m venv venv
          . venv/bin/activate
          pip install --upgrade pip
          pip install bandit
        '''
      }
    }

    stage('SAST Analysis') {
      steps {
        sh '''
          . venv/bin/activate
          bandit -f json -o bandit-output.json -r . || true
        '''
        // Gunakan parser Bandit JSON
        recordIssues tools: [bandit(pattern: 'bandit-output.json')]
        archiveArtifacts artifacts: 'bandit-output.json', fingerprint: true
      }
    }
  }
}

