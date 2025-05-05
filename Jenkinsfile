pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/Chaizaa/sast-demo-app.git', branch: 'master'
      }
    }

    stage('Run Bandit SAST') {
      steps {
        // 1) create & activate venv, install Bandit, run it
        sh '''
          python3 -m venv venv
          . venv/bin/activate
          pip install --upgrade pip
          pip install bandit
          bandit -r . -f xml -o bandit-output.xml || true
        '''

        // 2) Publish the XML report via Warnings NG
        recordIssues(
          enabledForFailure: true,
          tools: [bandit(pattern: 'bandit-output.xml')]
        )
      }
    }
  }
}

