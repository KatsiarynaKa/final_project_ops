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
                bat 'if not exist build\\classes mkdir build\\classes'
                bat '"%JAVA_HOME%\\bin\\javac" -d build\\classes Calculator.java'
            }
        }

        stage('Prepare Manifest') {
            steps {
            bat 'echo Main-Class: Main > build\\classes\\MANIFEST.MF'
            }
        }

        stage('Package') {
            steps {
            bat 'if not exist build\\jar mkdir build\\jar'
            bat 'cd build\\classes && "%JAVA_HOME%\\bin\\jar" cvmf MANIFEST.MF ..\\jar\\MyApplication.jar *'
            }
        }

        stage('Run the app') {
            steps {
               bat '"%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar'
            }
        }
    }
}
