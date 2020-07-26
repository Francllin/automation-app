pipeline {
   agent {
     docker {
       image 'ruby'
     }
   }

   stages {
      stage('Build') {
         steps {
            echo 'Remove lock e install bundler'
            sh 'rm -f Gemfile.lock'
            sh 'bundle install'
         }
        }
        stage('Test') {
         steps {
            echo 'rodar os teste'
            sh 'rake upload_apk'
            sh 'bundle exec cucumber -p emulador_sauce_android -p samsung_galaxy_s9'
         }
        }
        stage('UAT') {
         steps {
            echo 'Waiting For User Acceptance'
            input(message: 'Go to Production?', ok: 'Yes')
         }
        }

        stage('prod') {
            steps {
                echo 'Webapp is Ready :D'
         }
        }
   }
}