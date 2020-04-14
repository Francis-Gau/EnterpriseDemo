//Francis Gau 2020-04-14 Basic python pipeline
pipeline {
    agent none 
    parameters {
        string(name: 'Target', defaultValue: 'run', description: 'Run Target Value')
    }
    stages {
        stage('Build') {
            steps {
                sh 'pip install -r requirements.txt' 
            }
        }
        stage('Code Quality') {
            steps {
                sh 'pylint-fail-under --fail_under 5.0 *.py'
            }
        }
        stage('Code Quantity') {
            steps {
                sh 'find ./ -name "*.py" | wc -l'
            }
        }
        stage('Run') {
            when { 
                environment name: 'Target', value: 'run' 
            }
            steps {
                sh 'main.py phones text output'
                sh 'main.py tablets csv output'
                sh 'main.py laptops json output'
                sh 'main.py phones yaml output'
            }
        }
        stage('Package') {
            steps {
                sh 'zip app.zip *.py'
            }
        }
    }
}