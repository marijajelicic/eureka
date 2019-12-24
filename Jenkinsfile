pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "eureka:latest"
    options {
      gitLabConnection('https://github.com/marijajelicic/eureka.git')
    }
    stages {
        stage ('Docker') {
            when {
                branch 'master'
            }
            steps{
                script {
                    app = docker.build(DOCKER_IMAGE_NAME)
                    }
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
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                         
            }
        }
    }
}
