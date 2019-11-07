mavenVersion = 'Maven 3.5.0'
def upstreamJobs = ''
def MAVEN_TOOLCHAINS = '/opt/jenkins/tools/toolchains.xml'
def MAVEN_SETTINGS = '/opt/jenkins/tools/settings.xml'
def JAVA_6_HOME = '/opt/jenkins/tools/ibm-java-i386-60'
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
        mvnCmdOptions = "-U -PMVN_TOOLCHAINS --toolchains ${MAVEN_TOOLCHAINS} --settings ${MAVEN_SETTINGS} -Djava6.home=${JAVA_6_HOME}"
        mvnCmdOptionsWithoutToolchains = "-U --toolchains ${MAVEN_TOOLCHAINS} --settings ${MAVEN_SETTINGS} -Djava6.home=${JAVA_6_HOME}"
        gitCredentialsId = 'cibuilder_github'
        autoDeployBranch = "master"
        autoDeployBranchList = 'master,dev,task/upgrade-logging,ccqq,dev-ccqq,dev-webzone,cbfq,dev-hqq-ocp3.6,ccl2-dev,dev-cbfq,develop,cbfq-nv'
		skipTestsOption = "-Dmaven.test.skip=true -Djava6.home=${JAVA_6_HOME}"
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


				steps {

					script{

						println "Run Sonar"

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
