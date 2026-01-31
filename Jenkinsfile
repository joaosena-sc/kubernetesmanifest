node {
    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                // Verifique se o ID 'github' está correto no seu Jenkins (Manage Jenkins > Credentials)
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    
                    // Comandos sem variáveis de credenciais podem usar aspas duplas
                    sh "git config user.email joao0sena@yahoo.com.br"
                    sh "git config user.name joao.sena-sc"
                    sh "sed -i 's+joaosena22/project1:.*+joaosena22/project1:latest+g' deployment.yaml"
                    sh "git add ."

                    // IMPORTANTE: Use aspas simples (') aqui para que o Shell resolva as variáveis, não o Groovy
                    sh 'git commit -m "Done by Jenkins Job changemanifest: ${BUILD_NUMBER}" || echo "Sem mudanças"'
                    
                    // IMPORTANTE: Use aspas simples (') aqui para o PUSH
                    sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/joaosena-sc/kubernetesmanifest.git HEAD:main'
                }
            }
        }
    }
}
