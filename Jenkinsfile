pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        // sh 'mvn spring-javaformat:apply'
        // sh 'mvn clean'
      }
    }

    stage('Test') {
      steps {
        // sh 'mvn test'
      }
    }

    stage('Package') {
      steps {
        // sh 'mvn package'
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
		emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
	}
  }
}
