pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
            }
        }
         stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("httpd")
                    app.inside {
                        sh 'docker run -dit --name my-apache-app -p 9090:80 -v "$PWD":/usr/local/apache2/htdocs/ httpd:2.4'
                    }
                }
            }
        }
     
    } 
        
    
      
