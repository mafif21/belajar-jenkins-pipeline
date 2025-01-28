pipeline {
    agent none
    environment {
        AUTHOR = "Muhammad Afif"
        EMAIL = "afif.maliki21@gmail.com"
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }
    parameters {
        string(name: 'NAME', defaultValue: 'GUEST', description: 'What is your name ?')
        text(name: 'DESCRIPTION', defaultValue: '', description: 'Tell me about you ?')
        booleanParam(name: 'DEPLOY', defaultValue: false, description: 'Need to deploy ?')
        choice(name: 'SOCIAL_MEDIA', choices: ["FACEBOOK", "INSTAGRAM", "TWITTER"], description: 'Which social media ?')
        password(name: 'SECRET', defaultValue: '', description: 'Encrypt key')
    }
    triggers {
        // cron("*/2 * * * *")
        // pollSCM("*/5 * * * *")
        // upstream(upstreamProjects: 'job1,job2', threshold: hudson.model.Result.SUCCESS)
    }
    stages {
        stage("parameter") {
            agent {
                node {
                    label "linux && java11"
                }
            }

            steps {
                echo "Hello ${params.NAME}"
                echo "You are: ${params.DESCRIPTION}"
                echo "Want to deploy? ${params.DEPLOY ? 'yes': 'no'}"
                echo "Social Media: ${params.SOCIAL_MEDIA}"
                echo "Password: ${params.SECRET}"
            }
        }

        stage("prepare") {
            environment {
                APP = credentials("lelegoreng-password")
            }

            agent {
                node {
                    label "linux && java11"
                }
            }

            steps {
                echo "Username: ${APP_USR}"
                echo "Password: ${APP_PSW}"
                sh 'echo "App password : $APP_PSW" > "rahasia.txt"'
                echo "Author: ${env.AUTHOR}"
                echo "Email: ${env.EMAIL}"
                echo "Start job: ${env.JOB_NAME}"
                echo "Start build: ${env.BUILD_NUMBER}"
                echo "Branch name: ${env.BRANCH_NAME}"
            }
        }

        stage("build") {
            agent {
                node {
                    label "linux && java11"
                }
            }

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
            agent {
                node {
                    label "linux && java11"
                }
            }

            steps {
                script {
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