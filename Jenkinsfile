pipeline{
    agent any
    
    tools{
        maven 'localMaven'
    }
    stages{
        stage ('Build'){
            steps{
                echo "Building java project"
                sh 'mvn clean package'
            }
        }
        stage ('Upload to S3 Bucket') {
            steps{
                echo "Uploading the artifacts into S3 Bucket"
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'demobucketb5', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: true, selectedRegion: 'ap-south-1', showDirectlyInBrowser: false, sourceFile: '**/*.war', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'upload2S3', userMetadata: []
            }
        }
        stage ('Execute Playbook') {
            steps{
                ansiblePlaybook credentialsId: '9f4ccbec-2822-42be-b293-185a33da3328', disableHostKeyChecking: true, inventory: '/etc/ansible/hosts', playbook: '/etc/ansible/deployApp.yml'
            }
        }
    }
}
