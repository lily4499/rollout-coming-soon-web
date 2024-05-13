node {
    def app

    parameters {
        string(name: 'IMAGE_TAG',  description: 'Tag for the Docker image')
    }
    
    env.IMAGE = 'laly9999/coming-soon-website'
    env.IMAGE_TAG = "${env.BUILD_NUMBER}" 

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/lily4499/node-express-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'lily-git-credentials', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        sh "git config user.email konissil@gmail.com"
                        sh "git config user.name lily4499"
                        sh "cat rollout.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${IMAGE_TAG}+g' rollout.yml"
                        sh "cat rollout.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/rollout-coming-soon-web.git HEAD:main"
             }
         }
     }
  }
}
