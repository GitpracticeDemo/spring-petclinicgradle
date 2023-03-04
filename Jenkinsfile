
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
                sh 'export "PATH=/usr/lib/jvm/java-openjdk-1.8.0-amd64/bin:$PATH"'
                sh 'gradle --version'
                sh 'gradle'
                sh 'gradle tasks'
                sh 'gradle build'
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