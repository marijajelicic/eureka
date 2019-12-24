pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "eureka:latest"
    }
    scm {
        git {
            remote {
                github('marijajelicic/eureka')
                refspec('+refs/pull/*:refs/remotes/origin/pr/*')
            }
        }
    }
    stages {
        stage ('Docker') {
            when {
                branch 'master'
            }
            steps{
                script{
                    docker.build(DOCKER_IMAGE_NAME)
                }
            }
            post {
                failure {
                    emailext (
                        subject: "Job '${env.JOB_NAME} ${env.BUILD_NUMBER} - ${params.PARAMETAR}'",
                        body: """CI/CD pipeline greska u "Docker" fazi. Log fajl se moze videti na: href=${env.BUILD_URL} """,
                        to: "mjelicic@netcast.rs",
                        from: "mjelicic@netcast.rs"
                    )
                }
            }
        }
    }
}

