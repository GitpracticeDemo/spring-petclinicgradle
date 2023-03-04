pipeline {
    agent { label 'SPRING-PET' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/GitpracticeDemo/spring-petclinicgradle.git',
                    branch: 'scripted'
            }
        }
        stage('permission to gradel'){
            steps {
                echo 'Compile project'
                sh "chmod +x gradlew"
                sh "./gradlew clean build --no-daemon"
            }
        }   
        stage('package') {
             steps {
                 sh 'export "PATH=/usr/lib/jvm/java-openjdk-1.8.0-amd64/bin:$PATH"'
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