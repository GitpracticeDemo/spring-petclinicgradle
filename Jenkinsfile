pipeline {
    agent { label 'SPRING-PET' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/GitpracticeDemo/spring-petclinicgradle.git',
                    branch: 'scripted'
            }
        }
        stage('build'){
            steps {
                sh "gradlew build"
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