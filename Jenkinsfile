#!/usr/bin/env groovy

regions_script = '''
return ["select...", "hw", "cn"]
'''

targetEnvs_script = '''
return ["select...", "dev", "prod"]
''' 

sgSDKUrl_script =  '''
def getUrl() {
    def value = ""
        switch(REGION + TARGET_ENV) {
            case "hwdev":
                println "hwdev"
                value = "https://test-api.kingsoftgame.com"
                break
            case "hwprod": 
                println "hwprod"
                value = "https://safeapi.kingsoftgame.com"
                break
            case "cndev":
                println "cndev"
                value = "http://test-api-sgsdk.kingsoft.com"
                break
            case "cnprod":                    
                println "cnwprod"
                value = "https://api-sgsdk.kingsoft.com"
                break
        }
}
def url = getUrl()
return [url]
'''               




properties([
    parameters([
        [$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT',   name: 'REGION', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["ERROR"]'], script: [classpath: [], sandbox: false, script: regions_script]]],
        [$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT',   name: 'TARGET_ENV', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["ERROR"]'], script: [classpath: [], sandbox: false, script: targetEnvs_script]]],
        [$class: 'CascadeChoiceParameter', choiceType: 'PT_SINGLE_SELECT', name: 'SGSDK_URL', referencedParameters: 'REGION, TARGET_ENV', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["error"]'], script: [classpath: [], sandbox: false, script: sgSDKUrl_script]]]
    ])
])
pipeline{
    agent any
    
    stages{
        stage("Build"){
            steps{
                echo "========executing Building ========"
                echo "REGION is:" + params.REGION
                echo "TARGET_ENV is:" + params.TARGET_ENV
                echo "SGSDK_URL is:" + params.SGSDK_URL
                echo "APP_NAME is:" + params.APP_NAME
                echo "APP_ID is:" + params.APP_ID
            }
        }
    }
}