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
                    
                    def resultJson = parseJsonArray(featuresText.replaceAll(/[\r\n]/, ''))
                    
                    println "ClassXXX: " + resultJson.getClass().toString()
                    println "ClassXXX3: " + resultJson[0].getClass().toString()
                    
                    // resultJson.each {
                        // println “KEY=${it.key}” 
                    // }
                    
                    
                    build job: "my_pipeline_sub_job"
                }
            }
        }
    }
}

def parseJsonArray(String json) {
    def object = new JsonSlurper().parseText(json)
    
    println "XXXXXX11"
    for (int i=0; i<object.length; i++) {
        if(object instanceof groovy.json.internal.LazyMap) {    
            println "XXXXXX12"
            object[i] = new HashMap<>(object[i])
        }
    }
    
    return object
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