pipeline {
    agent { label 'SPRING-PET' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/GitpracticeDemo/spring-petclinicgradle.git',
                    branch: 'scripted'
            }
        }   
         stage('package') {
            steps {
                sh 'export "PATH=/usr/lib/jvm/java-openjdk-1.8.0-amd64/bin:$PATH"'
                sh 'chown ubuntu /opt/gradle-7.4.2'
                sh 'chmod o+w /opt/gradle-7.4.2'
                sh 'wget -O /tmp/gradle-7.4.2-bin.zip https://services.gradle.org/distributions/gradle-7.4.2-bin.zip'
                sh 'unzip /tmp/gradle-7.4.2-bin.zip -d /opt'
                
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/*.txt',
                                 allowEmptyArchive: true,
                                 fingerprint: true,
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}