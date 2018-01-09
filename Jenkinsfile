#!groovy

import groovy.json.JsonSlurper;

node {
    stage ('Clone') {
        echo 'now cloning'
        checkout scm
        sh "chmod +x gradlew"
    }
    stage ('Clean') {
        echo 'now cleaning'
        sh "./gradlew --stop"
        sh "./gradlew clean"
    }
    stage ('Build') {
        echo 'now building'
        sh "./gradlew assemble"
    }
    stage ('Test'){
        echo 'now testing'
        STATUS = sh ( 
            script: "curl -s -d \"id=5a43b6ec1b8b2332b3647363&path=${env.WORKSPACE}\" -H \"Content-Type: application/x-www-form-urlencoded\" -X POST http://localhost:3000/api/reports",
            returnStdout: true
            ).trim()
        def jsonSlurper = new JsonSlurper()
        def object = jsonSlurper.parseText(STATUS);
        if(object.success) {
           error(object.stacktrace)
        } else {
            echo object.stacktrace
        }
    }
    
}
