mavenVersion = 'Maven 3.5.0'
def upstreamJobs = ''
def upStreamJobsList = ['mb2/master' : 'MB1/master343']
String APPLICATION = env.JOB_NAME
println APPLICATION
autoDeployBranch = "master"
autoDeployBranchList = 'master,dev,task/upgrade-logging,ccqq,dev-ccqq,dev-webzone,cbfq,dev-hqq-ocp3.6,ccl2-dev,dev-cbfq,develop,cbfq-nv'
println BRANCH_NAME

if (upStreamJobsList[APPLICATION]) {
    upstreamJobs = upStreamJobsList[APPLICATION]
}

println "Job Run :" + APPLICATION + "Upstream job : " + upstreamJobs

pipeline {
    agent any
	
	
    parameters {
        booleanParam(name: 'forceDeploy', defaultValue: false, description: 'Forces the maven deploy of the current branch')
        booleanParam(name: 'performRelease', defaultValue: false, description: 'Performs a release of the current version of the application')
	booleanParam(name: 'activateSonar', defaultValue: true, description: 'Performs a release of the current version of the application')    

    
    }

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
