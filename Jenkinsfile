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
                dir ('app') {
                	sh 'docker build -t quay.io/rasulkarimov/myblog:latest . '
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
