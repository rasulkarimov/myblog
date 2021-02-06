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
                    sudo docker login -u $USERNAME -p $PASSWORD quay.io
                    """
                }
            }
        }
        stage("create docker image") {
            steps {
                echo " ============== start building image =================="
                dir ('app') {
                	sh 'sudo docker build -t quay.io/rasulkarimov/myblog:latest . '
                }
            }
        }
        stage("docker push") {
            steps {
                echo " ============== start pushing image =================="
                sh '''
                sudo docker push quay.io/rasulkarimov/myblog:latest
                '''
            }    
        }        

    }
}
