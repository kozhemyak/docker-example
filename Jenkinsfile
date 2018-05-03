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

                sh "rm -rf *-*.tar"

                sh "tar -cf somearchive-${BUILD_NUMBER}.tar ./src/"

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
                                "pattern": "(*)-(*).tar",
                                "target": "generic-local/{1}-{2}.tar",
                                "props": "status.type=DEV;status.stable=false",
                                "recursive": "false"
                            }
                        ]
                    }"""

                    // without spaces in PROPS

                    // Upload files to Artifactory:
                    def buildInfo = Artifactory.newBuildInfo()

                    buildInfo.env.capture = true
                    buildInfo.env.filter.addExclude("*FREAK_TEST*")


                    // test

                    //buildInfo.type = 'stable'

                    // buildInfo.env.collect() # To collect environment variables at any point in the script


                    buildInfo.append(artifactory.upload(uploadSpec))

                    // Merge the local download and upload build-info instances:
                    //buildInfo1.append buildInfo2

                    // Publish the merged build-info to Artifactory
                    artifactory.publishBuildInfo(buildInfo)

                    def scanConfig = [
                        'buildName'      : buildInfo.name,
                        'buildNumber'    : buildInfo.number,
                        'failBuild'      : false
                    ]

                    //def scanResult = artifactory.xrayScan scanConfig

                    //echo scanResult as String
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