#!groovy
properties([disableConcurrentBuilds()])

pipeline {
    agent { 
        label 'Cluster1'
        }
    triggers { pollSCM('* * * * *') }
    options {
        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
        timestamps()
    }
    
    stages {
        stage("docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: 'dockerhub-rasulkarimov', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                    docker login -u $USERNAME -p $PASSWORD
                    """
                }
            }
        stage("create docker image") {
            steps {
                echo " ============== start building image =================="
                dir ('app') {
                	sh 'docker build -t quay.io/rasulkarimov/myblog:latest . '
                }
            }
        }
        stage("docker push") {
            steps {
                echo " ============== start pushing image =================="
                sh '''
                docker push quay.io/rasulkarimov/myblog:latest
                '''
            }    
        }        

    }
}
