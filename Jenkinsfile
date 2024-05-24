pipeline {
    agent any
    tools {
        jdk 'Java'
    }

    environment {
        JAVA_HOME = tool 'Java'
    }
    stages {
        stage('Checking the app') {
            steps {
                git url: 'https://github.com/KatsiarynaKa/final_project.git', branch: 'main'
            }
        }

        stage('Compile the java file') {
            steps {
               bat buildCommand = "javac -d build Calculator.java"
            }
        }

        stage('Prepare Manifest') {
            steps {
               bat 'echo Calculator: Main > build\\classes\\MANIFEST.MF'
            }
        }
        
        stage('Package') {
            steps {
            bat packageCommand = "jar cvf Calculator.jar -C build ."
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/Calculator.jar', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            cleanWs()
        }
    }
}
