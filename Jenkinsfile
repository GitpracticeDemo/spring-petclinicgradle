
pipeline {
    agent { label 'SPRING-PET' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/GitpracticeDemo/spring-petclinicgradle.git',
                    branch: 'main'
            }
        }
        stage('package') {
            steps {
                sh 'export "PATH=/usr/lib/jvm/java-openjdk-1.0.8-amd64/bin:$PATH"'
                sh 'gradle test'
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}