pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                git(
                    url: 'https://github.com/MatiasRoje/datascientest_jenkins_exam-k8s.git',
                    branch: 'main',
                    credentialsId: 'github'
                )
            }
        }

        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                            sh "git config user.email rojechi@gmail.com"
                            sh "git config user.name MatiasRoje"
                            sh "cat root-service.yaml"
                            sh "sed -i 's+matiasroje/root-service:.*+matiasroje/rootservice:${DOCKERTAG}+g' root-service.yaml"
                            sh "cat root-service.yaml"
                            sh "git add ."
                            sh "git commit -m 'Done by Jenkins Job Update Manifest: ${env.BUILD_NUMBER}'"
                            sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/datascientest_jenkins_exam-k8s.git HEAD:main"
                        }
                    }
                }
            }
        }
    }
}