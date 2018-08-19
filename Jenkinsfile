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
                sshPublisher(publishers: [sshPublisherDesc(configName: 'staging_server', sshCredentials: [encryptedPassphrase: '{AQAAABAAAAAQY58XwJNf536+H5P5V3hYFEVI4/oWmp+4o/shpZw6pW8=}', key: '', keyPath: '', username: 'deploy'], transfers: [sshTransfer(excludes: '', execCommand: 'sudo /usr/bin/systemctl stop train-schedule && rm -rf /opt/train-schedule/* && unzip /tmp/trainSchedule.zip -d /opt/train-schedule && sudo /usr/bin/systemctl start train-schedule', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/tmp', remoteDirectorySDF: false, removePrefix: 'dist/', sourceFiles: 'dist/trainSchedule.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
        
        
    }
}
