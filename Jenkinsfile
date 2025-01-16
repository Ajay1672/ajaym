pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'aj', url: 'git@github.com:Ajay1672/ajaym.git'
            }
        }

        // stage('Clean') {
        //     steps {
        //         bat 'mvn clean'
        //     }
        // }

        // stage('Package') {
        //     steps {
        //         bat 'mvn package'
        //     }
        // }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonumonu') {
                    bat 'mvn sonar:sonar -Dsonar.projectKey=ajaym-java-application -Dsonar.host.url=http://localhost:9000'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    def qualityGate = waitForQualityGate()
                    if (qualityGate.status != 'OK') {
                        error "Quality Gate 'bugs' failed: ${qualityGate.status}"
                    } else {
                        echo "Quality Gate 'bugs' passed!"
                    }
                }
            }
        }

        stage('Upload to Nexus') {
            steps {
                script {
                    def artifactPath = 'demo-0.0.1-SNAPSHOT.jar'
                    def version = "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}"
                    def repositoryUrl = 'http://localhost:8081/repository/java-web/com/example/ajay/0.0.1/demo-0.0.1-SNAPSHOT.jar'

                    if (fileExists(artifactPath)) {
                        echo "Uploading artifact to Nexus..."
                        bat """
                            curl -v -u admin:admin --upload-file ${artifactPath} ${repositoryUrl}
                        """
                    } else {
                        error "The artifact ${artifactPath} does not exist!"
                    }
                }
            }
        }
    }
}
dd