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
                    
                    // resultJson.each {
                        // println “KEY=${it.key}” 
                    // }
                    
                    
                    build job: "my_pipeline_sub_job"
                }
            }
        }
    }
}

@NonCPS
def parseJsonText(String json) {
    def object = new JsonSlurper().parseText(json)
    if(object instanceof groovy.json.internal.LazyMap) {
        return new HashMap<>(object)
    }
    return object
}