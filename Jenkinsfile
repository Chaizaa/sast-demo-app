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
          bandit -f sarif -o bandit-output.sarif -r . || true
        '''
        // Gunakan parser Bandit JSON
        recordIssues tools: [sarif(pattern: 'bandit-output.sarif')]
        archiveArtifacts artifacts: 'bandit-output.sarif', fingerprint: true
      }
    }
  }
}





