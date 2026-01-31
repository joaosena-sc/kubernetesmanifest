sh """
    git config user.email "joao0sena@yahoo.com.br"
    git config user.name "joao.sena-sc"
    
    # Atualiza o arquivo
    sed -i 's+joaosena22/project1:.*+joaosena22/project1:latest+g' deployment.yaml
    
    git add deployment.yaml
    
    # Só tenta o commit se o 'git status' mostrar que algo mudou
    if [ -n "\$(git status --porcelain)" ]; then
        git commit -m "Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}"
        git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/joaosena-sc/kubernetesmanifest.git HEAD:main
    else
        echo "Nada mudou no arquivo. Pulando commit e push."
    fi
"""
