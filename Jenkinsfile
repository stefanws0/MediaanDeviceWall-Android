#!groovy

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
        sh 'curl -d “id=5a16e6e30a03df150e4feaa4&path=/Users/stefan/AndroidStudioProjects/Android_Jenkins_Prototype" -H "Content-Type: application/x-www-form-urlencoded" -X POST http://localhost:3000/reports'

    }
    
}