node {
  def app
    
    stage('Clone repository') {
  
        checkout scm
    }

    stage('Update GIT') {
      script {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          withCredentials([usernamePassword(credentialsId: 'githubpush', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
            sh "git config user.email eddie.d.lopez1@gmail.com"
            sh "git config user.name eddiedlopez"
            sh "cat vote-ui-deployment.yaml"
            sh "sed -i 's+eddiedlopez/vote-noarch.*+eddiedlopez/vote-noarch:${DOCKERTAG}+g' vote-ui-deployment.yaml"
            sh "cat vote-ui-deployment.yaml"
            sh "git add ."
            sh "git commit -m 'Done by Jenkins Job deployment: ${env.BUILD_NUMBER}'"
            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/vote-deploy.git HEAD:main"
          } 
        }
      }
   }
}
