pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        // sh 'mvn spring-javaformat:apply'
        // sh 'mvn clean'
		echo 'Build'
      }
    }

    stage('Test') {
      steps {
        // sh 'mvn test'
		echo 'Test'
      }
    }

    stage('Package') {
      steps {
        // sh 'mvn package'
		echo 'Package'
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
    always{
		emailext (
          subject: "INFO: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
          body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
          recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        )
	}
  }
}
