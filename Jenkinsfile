pipeline { 
    agent any
    environment {
        PATH = "${env.PATH}:${env.HOME}/.local/bin"
    }  
    stages { 
        stage('Checkout') { 
            steps { 
                git url: 'https://github.com/Chaizaa/sast-demo-app.git', branch: 
'master' 
            } 
        } 
        stage('Install Dependencies') { 
            steps { 
                sh 'pip install bandit' 
            } 
        } 
        stage('SAST Analysis') { 
            steps { 
                sh 'bandit -f xml -o bandit-output.xml -r . || true' 
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')] 
            } 
        } 
    } 
}  
