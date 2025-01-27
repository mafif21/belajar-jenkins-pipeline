pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("build") {
            steps {
                echo ("Get All Depedencies...")
            }
        }

        stage("test") {
            steps {
                echo ("Unit test starting...")
                sh("error")
            }
        }

        stage("deploy") {
            steps {
                echo ("Deploy to openshift")
            }
        }
    }
    post {
        always {
            echo "this action is always performed"
        }
        success {
            echo "this action is always performed when success"
        }
        failure {
            echo "this action is always performed when failure"
        }
        cleanup {
            echo "this action is always performed when everything is done"
        }
    }
}