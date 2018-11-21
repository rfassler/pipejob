pipeline {
    agent any
    stages{
        stage('Stage 1'){
            steps {
                bat 'echo Hello World'
            }
        }
        
        stage('Stage 2'){
            steps {
                script {
                    
                    for (String i : readFile('features.json').split("\r?\n")) {
                         println i
                    }
                    
                    
                }
            }
        }
    }
}