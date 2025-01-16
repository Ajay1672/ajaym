pipeline {
    agent any

    // environment {
    //     SLACK_CHANNEL = '#devops'  // Replace with the channel you want to post to 
    //     registryCredentials = 'ecr:ap-south-1:awscred'
    //     imageName = "533267404447.dkr.ecr.ap-south-1.amazonaws.com/vprofileappimg"
    //     vprofileRegistry = "https://533267404447.dkr.ecr.ap-south-1.amazonaws.com"
    // }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('Clone') {
            steps {
                git branch: 'master', credentialsId: 'a', url: 'git@github.com:Ajay1672/Docker-Jenkins-Java-Application.git'
            }
        }

        stage('Clean') {
            steps {
                bat 'cd WebApp && mvn clean'
            }
        }

        stage('Package') {
            steps {
                bat 'cd WebApp && mvn package'
            }
        }
        
    }

        // stage('Test Nexus URL') {
        //     steps {
        //         bat 'curl -v http://localhost:8081/#admin/repository/repositories:ajay-mvn'
        //     }
        // }

        // Uncomment and configure the following if you want to perform SonarQube analysis
        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonumonu') {
        //             bat 'cd WebApp && mvn sonar:sonar -Dsonar.projectKey=Docker-Jenkins-Java-Application \
        //                 -Dsonar.host.url=http://localhost:9000'
        //         }
        //     }
        // }

        // Uncomment and configure the following to enforce a Quality Gate
        // stage('Quality Gate') {
        //     steps {
        //         script {
        //             def qualityGate = waitForQualityGate()
        //             if (qualityGate.status != 'OK') {
        //                 error "Quality Gate 'bugs' failed: ${qualityGate.status}"
        //             } else {
        //                 echo "Quality Gate 'bugs' passed!"
        //             }
        //         }
        //     }
        // }

    //     stage('Upload to Nexus') {
    //         steps {
    //             script {
    //                 def artifactPath = 'WebApp/target/ajay-0.0.1-SNAPSHOT.jar'
    //                 def version = "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}"
    //                 def repositoryUrl = 'http://localhost:8081/repository/ajay-mvn/com/example/ajay/0.0.1/ajay-0.0.1-SNAPSHOT.jar'

    //                 if (fileExists(artifactPath)) {
    //                     echo "Uploading artifact to Nexus..."
    //                     bat """
    //                         curl -v -u admin:admin --upload-file ${artifactPath} ${repositoryUrl}
    //                     """
    //                 } else {
    //                     error "The artifact ${artifactPath} does not exist!"
    //                 }
    //             }
    //         }
    //     }

    // }

    // post {
    //     always {
    //         script {
    //             // Define color map for Slack
    //             def COLOR_MAP = [
    //                 'SUCCESS': 'good',    // Green for success
    //                 'FAILURE': 'danger',  // Red for failure
    //                 'UNSTABLE': 'warning' // Yellow for unstable builds
    //             ]

    //             // Determine the build status
    //             def buildStatus = currentBuild.result ?: 'SUCCESS'  // Default to 'SUCCESS' if no result is set

    //             // Send the Slack message with the appropriate color
    //             slackSend(
    //                 channel: SLACK_CHANNEL,
    //                 color: COLOR_MAP[buildStatus], 
    //                 message: "Build #${env.BUILD_ID} ${buildStatus} - ${env.JOB_NAME} (${env.BUILD_URL})"
    //             )
    //         }
    //     }
    // }
}



//  aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 533267404447.dkr.ecr.ap-south-1.amazonaws.com

//  docker push 533267404447.dkr.ecr.ap-south-1.amazonaws.com/vprofileappimg:5
