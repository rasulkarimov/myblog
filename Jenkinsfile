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
        stage("sudo docker login") {
            steps {
                echo " ============== docker login =================="
                withCredentials([usernamePassword(credentialsId: 'dockerhub-rasulkarimov', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                    docker login -u $USERNAME -p $PASSWORD
                    """
                }
            }
        }
        stage("create docker image") {
            steps {
                  checkout scm
                  def customImage = docker.build("rasulkarimov/myblog", "app")
                  customImage.push()
            }
        }
    }
}
