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
                echo ("build 1")
                echo ("build 2")
                echo ("build 3")
            }
        }

        stage("test") {
            steps {
                echo ("Unit test starting...")
                echo ("ut 1")
                echo ("ut 2")
                echo ("ut 3")
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