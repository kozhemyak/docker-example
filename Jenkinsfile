pipeline {
    agent any
    environment {
        FREAK_TEST='TESTTESTETST'
    }
    stages {

        // Checkout from repository
        stage('Clone (GIT)') {
            steps {
                git url: 'https://github.com/kozhemyak/docker-example.git'
            }
        }

        // Build the image
        stage('Create Fake Archive'){
            steps {
                echo "---------------------------------"

                //sh "rm -rf *-*.tgz" // For quick test

                //sh "tar -cf somearchive-${BUILD_NUMBER}.tar ./src/"

                echo "---------------------------------"
            }
        }

        //
        //ls
        //docker info
        //docker build -t katacoda/jenkins-demo:${BUILD_NUMBER} .
        //docker tag katacoda/jenkins-demo:${BUILD_NUMBER} katacoda/jenkins-demo:latest
        //docker images

        stage('Push to Artifactory (Script)'){
            steps {
                script{
                    def artifactory = Artifactory.server('Docker-Example-Registry-01')
                    def uploadSpec = """{
                        "files": [
                            {
                                "pattern": "*.tgz",
                                "target": "helm/",
                                "props": "status=DEV;status.stable=false",
                                "recursive": "false"
                            }
                        ]
                    }"""
                    // without spaces in PROPS
                    // Upload files to Artifactory:
                    def buildInfo = Artifactory.newBuildInfo()
                    buildInfo.env.capture = true
                    buildInfo.env.filter.addExclude("*FREAK_TEST*")
                    artifactory.upload spec: uploadSpec, buildInfo: buildInfo
                    artifactory.publishBuildInfo buildInfo

                }
            }
        }

        // Wait for my contribution
        stage('Waiting') {
            steps {
                sleep 1
            }
        }
    }
}