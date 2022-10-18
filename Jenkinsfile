node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'gittoken', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        echo "${params.DOCKERTAG}" 
                        sh "git config user.email roshmi.gopa@gmail.com"
                        sh "git config user.name RoshmiB"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i.bak 's+roshmi/gitopsk8stest.*+roshmi/gitopsk8stest:${params.DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://RoshmiB:${GIT_PASSWORD}@github.com/RoshmiB/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
