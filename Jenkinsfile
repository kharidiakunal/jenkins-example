mavenVersion = 'Maven 3.5.0'
def upstreamJobs = ''
def upStreamJobsList = ['MB2/master' : ['MB1/master']]
String APPLICATION = env.JOB_NAME
println APPLICATION

if (upStreamJobsList[APPLICATION]) {
    upstreamJobs = upStreamJobsList[APPLICATION]
}

println "Job Run :" + APPLICATION + "Upstream job : " + upstreamJobs

pipeline {
    agent any

    triggers {
        upstream(
                upstreamProjects: "${upstreamJobs}",
                threshold: hudson.model.Result.SUCCESS)
    }
   
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
