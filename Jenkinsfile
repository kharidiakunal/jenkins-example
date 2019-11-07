pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                script {
                   //println getPRTargetBranchInfoFromGithubApi('kharidiakunal')
                    def changeid = 1
                   def githupApiCurlResponse =""
                   withCredentials([usernamePassword(credentialsId: '595e1606-e16f-4d35-99c4-b678ce9e6d34', passwordVariable: 'GITHUB_TOKEN', usernameVariable: 'GITHUB_USERNAME')]) {
                     def REPOSITORY = JOB_NAME.replace("/${env.BRANCH_NAME}","")
                     println "repository" + REPOSITORY
                     def githubApiGetPREndpoint = "https://githubifc.iad.ca.inet/api/v3/repos/${REPOSITORY}/pulls/${changeid}"
                     println githupApiCurlResponse = sh(script:"curl -v -k -u ${GITHUB_USERNAME}:${GITHUB_TOKEN} ${githubApiGetPREndpoint}", returnStdout:true)   
                   }
                }    
            }
        }
    }
}

