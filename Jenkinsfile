pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('DeployToProduction') {
            when {
             branch 'master'   
            }
            steps {
             input 'Does the deploy is correct ?'
                milistone(1)
                withCredentials([usernamePassword(credentialsId : 'webserver_login', usernameVariable:'USERNAME', passwordVariable: 'USERPASS')
                                                  sshPublisher(
                                                      failOnError: true,
                                                      continueOnError: false,
                                                      publishers: [
                                                          sshpublisherDesc (
                                                              configName :'deploy'
                                                              sshCredentials : [
                                                                  username : "$USERAME",
                                                                  encryptedPassphrase: "$USERPASS"
                                                                  ],
                                                              transfer :[
                                                                  sshTransfer (
                                                                      sourceFiles : '/dist/trainScheduler',
                                                                      removePrefix: 'dist/',
                                                                      remoteDirectory: '/tmp',
                                                                      execCommand 
            }
        }
    }
}
