mavenVersion = 'Maven 3.5.0'
def upStreamJobsList = ['mb1/develop' : ['mb2/develop']]
String APPLICATION = env.JOB_NAME
println APPLICATION

pipeline {
    agent any

   
    stages {
        stage ('Compile Stage') {

            steps {
				sh 'echo compile stage'
            }
        }

        stage ('Testing Stage') {

            steps {
				sh 'echo Testing Stage'
            }
        }


        stage ('Deployment Stage') {
            steps {
				sh 'echo Deployment Stage'
            }
        }
    }
}
