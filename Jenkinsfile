pipeline {
    agent any 
    stages {
        stage('removing old files') { 
            steps {

                sh "sudo rm -rvf /var/www/html/test/*"
                sh "sudo rm -rvf /var/www/html/test/.git*"
                sh "sudo rm -rvf /var/www/html/test/.e*"
                sh "sudo rm -rvf /var/www/html/test/.s*"
                sh " sudo touch script.sh"
                
            }
        }
        stage('Cloning repo') { 
            steps {
                sh " cd /var/www/html/test"
                sh " sudo git clone https://github.com/pemba3690/test.git /var/www/html/test/"
             
                sh " sudo chmod -R a+x script.sh "
                sh " sudo ./script.sh"
                 sh " sudo php artisan key:generate"
		        sh " sudo php artisan migrate "
                sh " sudo php artisan db:seed "
                sh " sudo php artisan storage:link "
                //
            }
        }
        stage('Reloading code') { 
            steps {
                sh " sudo chmod -R o+w storage/ "
                sh "sudo systemctl reload apache2"
                
            }
        }
    }
}
