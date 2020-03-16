def previousSucess
def count
def skipping = false
def testPass = false
pipeline {
	agent any
	stages {
		stage('Phase 1') {
			steps {
				script {
					count = readFile("D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/Count.txt").trim().toInteger()
					previousSucess = readFile("D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/PreviousSucess.txt").trim()
					echo "${count}"
					echo "${previousSucess}"
					echo "$env.GIT_COMMIT"
					if( previousSucess == "" ){
						echo 'No previous sucess build, going to build.'
					}
					else{
						if( count >=8 ){
							echo "${count}"
							echo 'Having 8 commits, going to build.'
							writeFile(file: "D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/Count.txt", text: "0")
						}
						else{
							newCount = count + 1
							echo "${newCount}"
							writeFile(file: "D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/Count.txt", text: newCount.toString())
							echo 'increment count and exiting.'
							skipping = true
						}
					}
				}
			}
		}
		stage('Build') {
			steps {
				script {
					if (!skipping){
						echo 'Building'
						sh 'mvn spring-javaformat:apply'
						sh 'mvn clean'
					}
				}
			}
		}

		stage('Test') {
			steps {
				script {
					if (!skipping){
						echo 'Testing..'
						sh 'mvn test' 
						writeFile(file: "D:/CONCORDIA/2020/20 01 WINTER/SOEN 345/Assignments/06/q3/spring-petclinic/PreviousSucess.txt", text:  env.GIT_COMMIT)
					}
				}
			}
		}

		stage('Package') {
			steps {
				script {
					if (!skipping){
						echo 'Packaging'
						sh 'mvn package'
					}
				}  
			}
		}

		stage('Deploy') {
			steps {
				script{
					if (!skipping){
						echo 'Deploying.'
					}
				}
			}
		}
	}
	post {
    	failure {
			script {
				sh 'git bisect start'
			}
			script {
				def unstable = env.GIT_COMMIT
				sh 'git bisect bad $unstable'
			}
			script {
				sh 'git bisect good $previousSucess'
			}
			script {
				sh 'git bisect run mvn clean test'
				sh 'git bisect reset'
			}
    	}
	}
}