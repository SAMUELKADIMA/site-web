pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/SAMUELKADIMA/site-web.git'
            }
        }
        
        stage('Test') {
            steps {
                echo 'Vérification du code HTML...'
                sh '''
                    if grep -q "<!DOCTYPE html>" index.html; then
                        echo "✅ Test HTML réussi"
                    else
                        echo "❌ Erreur: index.html n'est pas valide"
                        exit 1
                    fi
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                echo 'Déploiement du site web...'
                sh '''
                    # Créer le dossier de déploiement (sans sudo)
                    mkdir -p /var/www/site-web
                    
                    # Copier les fichiers
                    cp -r * /var/www/site-web/
                    
                    # Configurer les permissions
                    chmod -R 755 /var/www/site-web
                    
                    echo "✅ Site déployé avec succès !"
                '''
            }
        }
    }
    
    post {
        success {
            echo '🎉 Pipeline terminé avec succès !'
        }
        failure {
            echo '❌ Le pipeline a échoué !'
        }
    }
}
