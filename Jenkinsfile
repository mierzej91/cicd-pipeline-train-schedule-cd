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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'staging_server', sshCredentials: [encryptedPassphrase: '{AQAAABAAAAAQccEOSm8xdfqJhiVU6oNYltVT0/bHGCmIXsH+DUA2TwA=}', key: '', keyPath: '', username: 'deploy'], transfers: [sshTransfer(excludes: '', execCommand: 'systemctl stop train-schedule && unzip /tmp/trainSchedule.zip -d /opt/train-schedule && systemctl start train-schedule', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/tmp/', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/trainSchedule.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
        
        
    }
}
