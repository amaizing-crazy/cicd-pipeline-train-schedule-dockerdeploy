pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("amaizingcrazy/train-schedule")
                    app.inside {
                        sh 'sleep 20'
                        sh 'echo $(curl 127.0.0.1:8080)'
                    }
                }
            }
        }
    }    
}
