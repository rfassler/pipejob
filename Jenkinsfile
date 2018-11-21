import groovy.json.JsonSlurper

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
                    
                    def featuresText = readFile('features.json')
                    
                    println "Features=${featuresText}"
                    
                    for (String i : featuresText.split("\r?\n")) {
                         println i
                    }
                    
                    def jsonSlurper = new JsonSlurper()
                    
                    // def resultJson = jsonSlurper.parseText(featuresText.replaceAll(/[ ]/, ''))
                    
                    // resultJson.each {
                        // print “KEY=${it.key}” 
                    // }
                    
                }
            }
        }
    }
}