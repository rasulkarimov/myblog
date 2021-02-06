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
        stage("create docker image") {
            steps {
                echo " ============== start building image =================="
                dir ('myblog/app') {
                        sh 'pwd'
                        sh 'ls -l'
                	sh 'docker build -t quay.io/rasulkarimov/myblog:latest . '
                }
            }
        }        

    }
}
