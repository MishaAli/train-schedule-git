pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh "${tool name: 'gradle4.6', type: 'hudson.plugins.gradle.GradleInstallation'}/bin/gradle build --no-daemon"
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
       stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("misha/train-schedule")
                    app.inside {
                        sh 'echo $(curl localhost:3000)'
                    }
                }
            }
        }
    }
}
