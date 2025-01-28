pipeline {
    agent {
        node {
            label "linux && java11"
        }
    }
    stages {
        stage("build") {
            steps {
                script {
                    for (int i = 0; i < 5; i++) {
                        echo "Loading ${i}"
                    }
                }
                echo "Get All Depedencies..."
                sh "./mvnw clean compile test-compile"
                echo "Finish build"
            }
        }

        stage("test") {
            steps {
                script : {
                    def data = [
                        "first_name": "muhammad",
                        "last_name": "afif"
                    ]
                    writeJSON(file: "data.json", json: data)
                }

                echo "Unit test starting..."
                sh "./mvnw test"
                echo "Finish test"
            }
        }

        stage("deploy") {
            steps {
                echo "Deploy to openshift"
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