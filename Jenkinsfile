//Francis Gau 2020-04-14 Basic python pipeline
pipeline {
    agent any
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
                script{
                sh 'python3 main.py phone text output'
                sh 'python3 main.py tablet csv output'
                sh 'python3 main.py laptop json output'
                sh 'python3 main.py phone yaml output'
                }
            }
        }
        stage('Package') {
            steps {
                sh 'zip app.zip *.py'
            }
        }
    }
}