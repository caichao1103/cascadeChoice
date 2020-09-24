#!/usr/bin/env groovy

regions_script = '''
return ["select...", "hw", "cn"]
'''

targetEnvs_script = '''
return ["select...", "dev", "prod"]
''' 

Reg_script =  '''
def reg = TARGET_ENV + REGION
return [reg]
'''               




properties([
    parameters([
        [$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT',   name: 'REGION', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["ERROR"]'], script: [classpath: [], sandbox: false, script: regions_script]]],
        [$class: 'ChoiceParameter', choiceType: 'PT_SINGLE_SELECT',   name: 'TARGET_ENV', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["ERROR"]'], script: [classpath: [], sandbox: false, script: targetEnvs_script]]],
        [$class: 'CascadeChoiceParameter', choiceType: 'PT_SINGLE_SELECT',name: 'REG', referencedParameters: 'REGION, TARGET_ENV', script: [$class: 'GroovyScript', fallbackScript: [classpath: [], sandbox: false, script: 'return ["error"]'], script: [classpath: [], sandbox: false, script: Reg_script]]]
    ])
        
        
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
            }
        }
    }
}