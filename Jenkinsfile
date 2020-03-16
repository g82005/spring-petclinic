pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn spring-javaformat:apply'
        sh 'mvn clean'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

    stage('Deploy') {
      when {
        branch 'master'
      }
      steps {
        echo 'Deploying'
      }
    }

  }
  post {
    success{
		emailext (
          subject: "INFO: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """INFO: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':
		  Check console output at ${env.BUILD_URL} for job ${env.JOB_NAME} [${env.BUILD_NUMBER}]""",
          recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        )
	}
  }
}
