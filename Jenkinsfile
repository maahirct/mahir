pipeline {
    agent none

    stages {
        stage('build') {
            agent {
                label 'buildnode'
            }
            steps {
                deleteDir()

                sh '''
                    git clone https://github.com/maahirct/mahir.git
                    ls -la
                '''

                stash name: 'webpage', includes: 'mahir/**'
            }
        }

        stage('deploy') {
            agent {
                label 'deloynode'
            }
            steps {
                deleteDir()

                unstash 'webpage'

                sh '''
                    rm -rf /var/www/html/*
                    cp -r mahir/* /var/www/html/
                    ls -la
                '''
            }
        }
    }
}
