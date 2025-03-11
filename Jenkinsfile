pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
                sh 'git clone -b dev https://github.com/BhanuBolligorla/taxi-booking.git'
            }
        }
        stage('check') {
            steps {
                dir ("taxi-booking") {
                    sh ('ls -l')
                    sh ('mvn package')
                }
            }
        }
        stage('copy') {
            steps {
                dir ("taxi-booking/target") {
                    sh 'mv *.war ${JOB_NAME}-${BUILD_ID}.war'
                    sh 'cp *.war /opt/apache-tomcat-9.0.100/webapps'
                }
            }
        }
        stage('backup') {
            steps {
                dir ("taxi-booking/target") {
                    sh 'cp *.war /home/'
                }
            }
        }
    }
}

