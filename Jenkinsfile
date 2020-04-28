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
                        sh 'sleep 10'
                        sh 'echo $(curl localhost:8080)'
                    }
                }
            }
        }
    }    
}
