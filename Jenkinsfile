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
                    
                    def resultJson = parseJsonText(featuresText.replaceAll(/[\r\n]/, ''))
                    
                    println "ClassXXX: " + resultJson.getClass().toString()
                    
                    // resultJson.each {
                        // println “KEY=${it.key}” 
                    // }
                    
                    
                    build job: "my_pipeline_sub_job"
                }
            }
        }
    }
}

def parseJsonText(String json) {
    def object = new JsonSlurper().parseText(json)
    println "XXXXXX1"
    if(object instanceof groovy.json.internal.LazyMap) {
        println "XXXXXX2"
        return new HashMap<>(object)
    }
    return object
}