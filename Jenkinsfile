pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                sh 'git clone -b main https://github.com/Sai-Munagoti/pipeline.git'
            }
        }
        stage('check') {
            steps {
                dir ("pipeline") {
                    sh ('ls -l')
                    sh ('mvn package')
                }
            }
        }
        stage('copy') {
            steps {
                dir ("pipeline/target") {
                    sh 'mv *.war ${JOB_NAME}-${BUILD_ID}.war'
                    sh 'cp *.war /opt/apache-tomcat-9.0.100/webapps'
                }
            }
        }
        stage('backup') {
            steps {
                dir ("pipeline/target") {
                    sh 'cp *.war /home/'
                }
            }
        }
    }
}

