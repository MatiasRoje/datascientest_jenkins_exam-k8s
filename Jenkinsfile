node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email rojechi@gmail.com"
                        sh "git config user.name MatiasRoje"
                        //sh "git switch master"
                        sh "cat root-service.yaml"
                        sh "sed -i 's+matiasroje/root-service:.*+matiasroje/rootservice:${DOCKERTAG}+g' root-service.yaml"
                        sh "cat root-service.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/datascientest_jenkins_exam-k8s.git HEAD:main"
      }
    }
  }
}
}
