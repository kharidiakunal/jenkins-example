pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                //println getPRTargetBranchInfoFromGithubApi('kharidiakunal')
                def githupApiCurlResponse =""
    withCredentials([usernamePassword(credentialsId: 'kharidiakunal', passwordVariable: 'GITHUB_TOKEN', usernameVariable: 'GITHUB_USERNAME')]) {
        def REPOSITORY = JOB_NAME.replace("/${env.BRANCH_NAME}","")
        def githubApiGetPREndpoint = "https://githubifc.iad.ca.inet/api/v3/repos/${REPOSITORY}/pulls/${env.CHANGE_ID}"
        def githupApiCurlResponse = bat(returnStdout:true , script:"curl -v -k -u ${GITHUB_USERNAME}:${GITHUB_TOKEN} ${githubApiGetPREndpoint}")
    }
            }
        }
    }
}

