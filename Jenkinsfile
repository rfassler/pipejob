import groovy.json.JsonSlurper

pipeline {
    
    agent any

    stages{

        stage('Build'){
            steps {
                bat 'echo Hello World'
            }
        }
        
        stage('Feature Testing'){
            steps {
                script {
                    
                    def featuresText = readFile('features.json')
                    
                    println "Features=${featuresText}"
                    
                    for (String i : featuresText.split("\r?\n")) {
                         println i
                    }
                    
                    def resultJson = parseJsonArray(featuresText.replaceAll(/[\r\n]/, ''))
                    
                    def jobs = [:]
                    
                    resultJson.each {
                        //println it.toString()
                        
                        def name = it['name']
                        
                        jobs["Stage job_${name}"] = {

                            stage ("Test Feature: ${name}") { 
                            
                                build job: "my_pipeline_sub_job", parameters: [[$class: 'StringParameterValue', name: 'job_name', value: "${name}"]]

                            }
                        }
                        
                        parallel jobs
                    }
                }
            }
        }
        
        stage('Publish Report') {
            
            steps {
                publishHTML (target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'index.html',
                    reportName: "Feature X Report"
                ])
                
                publishHTML (target: [
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: '.',
                    reportFiles: 'index.html',
                    reportName: "Feature Y Report"
                ])
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