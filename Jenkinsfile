pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                script {
                   //println getPRTargetBranchInfoFromGithubApi('kharidiakunal')
                   def githupApiCurlResponse =""
                   withCredentials([usernamePassword(credentialsId: '595e1606-e16f-4d35-99c4-b678ce9e6d34', passwordVariable: 'GITHUB_TOKEN', usernameVariable: 'GITHUB_USERNAME')]) {
                     def REPOSITORY = JOB_NAME.replace("/${env.BRANCH_NAME}","")
                    def githubApiGetPREndpoint = "https://githubifc.iad.ca.inet/api/v3/repos/${REPOSITORY}/pulls/${env.CHANGE_ID}"
                    githupApiCurlResponse = sh(script:"curl -v -k -u ${GITHUB_USERNAME}:${GITHUB_TOKEN} ${githubApiGetPREndpoint}", returnStdout:true)   
                   }
                }    
            }
        }
    }
}

