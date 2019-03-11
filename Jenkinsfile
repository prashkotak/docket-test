pipeline {
    agent none
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
            }
        }
		stage('DeployToStaging') {
            when {
                branch 'master'
            }
			steps {
                withCredentials([usernamePassword(credentialsId: 'webserver', usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    sshPublisher(
                        failOnError: true,
                        continueOnError: false,
                        publishers: [
                            sshPublisherDesc(
                                configName: 'master',
                                sshCredentials: [
                                    username: "$USERNAME",
                                    encryptedPassphrase: "$USERPASS"
                                ], 
                                transfers: [
                                    sshTransfer(
                                        sourceFiles: 'tmp/trainSchedule.zip',
                                        removePrefix: 'tmp/',
                                        remoteDirectory: '/tmp',
                                        execCommand: 'docker pull httpd'
                                    )
                                ]
                            )
                        ]
                    )
                }
            }
        }
	}    
}
