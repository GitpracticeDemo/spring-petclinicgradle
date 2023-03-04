
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
                sh 'wget -c https://services.gradle.org/distributions/gradle-7.4.2-bin.zip -P /tmp'
                sh 'sudo apt install unzip -y'
                sh 'sudo unzip -d /opt/gradle /tmp/gradle-7.4.2-bin.zip -y'
                
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