pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'mvn spring-javaformat:apply'
        echo 'mvn clean'
      }
    }

    stage('Test') {
      steps {
        echo 'mvn test'
      }
    }

    stage('Package') {
      steps {
        echo 'mvn package'
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
		echo "post"
	}
  }
}
