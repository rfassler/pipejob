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
                    
                    resultJson.each {
                        println it.toString()
                        
                        stage ("branch_1") { 
                        
                            build job: "my_pipeline_sub_job"
                            
                        }
                    }
                }
            }
        }
    }
}

def parseJsonArray(String json) {
    def object = new JsonSlurper().parseText(json)
    
    for (i=0; i<object.size(); i++) {
        if(object.get(i) instanceof groovy.json.internal.LazyMap) {    
            object.putAt(i, new HashMap<>(object.get(i)))
        }
    }
    
    return object
}