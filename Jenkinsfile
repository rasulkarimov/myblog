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
                echo "Test line"
            }
        }
        stage("create docker image") {
            steps {
                echo " ============== start building image =================="
            }
        }
        stage("docker push") {
            steps {
                echo " ============== start pushing image =================="
            }
        }
    }
}
