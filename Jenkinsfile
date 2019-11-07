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
	
    environment {
        mvnCmdOptions = "-U -PMVN_TOOLCHAINS --toolchains"
        mvnCmdOptionsWithoutToolchains = "-U --toolchains"
        gitCredentialsId = 'cibuilder_github'
        autoDeployBranch = "master"
        autoDeployBranchList = 'master,dev,task/upgrade-logging,ccqq,dev-ccqq,dev-webzone,cbfq,dev-hqq-ocp3.6,ccl2-dev,dev-cbfq,develop,cbfq-nv'
		skipTestsOption = "-Dmaven.test.skip=true"
        IS_UNIX = isUnix()
        baseReleaseWorkingDirectory = '-DbaseReleaseWorkingDirectory=F:/Data/tmp/intact-release'
        mvnAutoRelease = "-Dsha1=-\$BUILD_TIMESTAMP -Dchangelist="

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
	    
	// Run Sonar starts here
	    
	stage("Run Sonar") {

				when {

					expression { params.activateSonar }

				}

				steps {

					script{

						sonarBranch = ""

						sonarArguments = ""
						gitCredentialsId = "kharidiakunal"
						rootSonarBranch = ""
						targetSonarBranch = ""
						
						if(env.CHANGE_ID){

							// PR analysis

							REPOSITORY = JOB_NAME.replace("/${env.BRANCH_NAME}","")

							targetBranchName = getPRTargetBranchInfoFromGithubApi(gitCredentialsId)

							sonarArguments = "${mvnCmdOptions} -Dsonar.pullrequest.provider=github -Dsonar.host.url=${sonarHostUrl} -Dsonar.pullrequest.key=${env.CHANGE_ID} -Dsonar.pullrequest.branch=${env.BRANCH_NAME} -Dsonar.pullrequest.github.repository=${REPOSITORY} -Dsonar.pullrequest.base=${targetBranchName} -Dsonar.projectKey=${projectGroupId}:${projectArtifactId} ${sonarBranch}"

						}else{

							sonarBranchNameArgs = ""

							sonarBranchTargetNameArgs = ""

							// Branch analysis

							if(env.BRANCH_NAME.toUpperCase() !=  rootSonarBranch.toUpperCase()) {

								sonarBranchNameArgs = "-Dsonar.branch.name=${env.BRANCH_NAME}"

								if(env.BRANCH_NAME.toUpperCase() != targetSonarBranch.toUpperCase() ) {

									sonarBranchTargetNameArgs = "-Dsonar.branch.target=${targetSonarBranch}"

								}	

							}



							sonarArguments = "${mvnCmdOptions} -Dsonar.projectKey=${projectGroupId}:${projectArtifactId} ${sonarBranchNameArgs} ${sonarBranchTargetNameArgs}"

						}

					}

					withSonarQubeEnv("${sonarQubeServer}") {

						bat "mvn sonar:sonar ${sonarArguments}"

					}

				}

			}
	    
		// Run Sonar ends here
	    
	    
        stage ('Deployment Stage') {
            steps {
				sh 'echo Deployment Stage'
            }
        }
	}
}
