pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                //println getPRTargetBranchInfoFromGithubApi('kharidiakunal')
                githupApiCurlResponse =""
    withCredentials([usernamePassword(credentialsId: 'kharidiakunal', passwordVariable: 'GITHUB_TOKEN', usernameVariable: 'GITHUB_USERNAME')]) {
        REPOSITORY = JOB_NAME.replace("/${env.BRANCH_NAME}","")
        githubApiGetPREndpoint = "https://githubifc.iad.ca.inet/api/v3/repos/${REPOSITORY}/pulls/${env.CHANGE_ID}"
        githupApiCurlResponse = bat(returnStdout:true , script:"curl -v -k -u ${GITHUB_USERNAME}:${GITHUB_TOKEN} ${githubApiGetPREndpoint}")
    }
            }
        }
    }
}

