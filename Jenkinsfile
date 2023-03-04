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
                sh 'wget -O /tmp/gradle-7.4.2-bin.zip https://services.gradle.org/distributions/gradle-7.4.2-bin.zip'
                sh 'mkdir /opt/gradle-7.4.2'
                sh 'unzip /tmp/gradle-7.4.2-bin.zip -d /opt'
                
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/opt/gradle-7.4.2',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}