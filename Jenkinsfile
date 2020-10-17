pipeline{
    agent{
        docker {
            image "maven:3-alpine"
            args "-v /root/.m2:/root/.m2"
        }
    }
    stages{
        stage("Test") {
            ssh "mvn test"
        }
        stage("build"){
            steps{
                sh "mvn -B -DskipTests clean package"
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========A executed successfully========"
                }
                failure{
                    echo "========A execution failed========"
                }
            }
        }
        stage("Deliver"){
            steps{
                sh "./jenkins/scripts/deliver.sh"
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++ executed successfully++++===="
                }
                failure{
                    echo "====++++ execution failed++++===="
                }
        
            }
        }
    }
    post{
        always{
            echo "========always========"
            junit "target/surefire-reports/*.xml"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}