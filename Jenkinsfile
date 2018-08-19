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
       
        stage('Staging') {
            steps {
                echo 'Deploy To the Staging server'
                sshPublisher(publishers: [sshPublisherDesc(configName: 'staging_server', sshCredentials: [encryptedPassphrase: '{AQAAABAAAAAQ0JrmvQgKrgYiE9lb2xX1OwAlaD5qckWz4SOL9dYOLBU=}', key: '', keyPath: '', username: 'deploy'], transfers: [sshTransfer(excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/opt/train-schedule/', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/trainSchedule.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sh 'systemctl stop train-schedule && unzip /tmp/trainSchedule.zip -d /opt/train-schedule && systemctl start train-schedule'
            }
        }
        
        
        
    }
}
