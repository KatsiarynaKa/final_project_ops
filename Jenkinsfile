pipeline {
    agent any

    tools {
        jdk 'Java' // Ensure you have configured a JDK named 'Java' in Jenkins
    }

    environment {
        JAVA_HOME = tool name: 'Java', type: 'JDK'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/KatsiarynaKa/final_project.git', branch: 'main'
            }
        }

        stage('Compile') {
            steps {
                bat """
                    if not exist build\\classes mkdir build\\classes
                    "%JAVA_HOME%\\bin\\javac" -d build\\classes Calculator.java
                """
            }
        }

        stage('Prepare Manifest') {
            steps {
                bat """
                    echo Main-Class: Calculator > build\\classes\\MANIFEST.MF
                """
            }
        }

        stage('Package') {
            steps {
                bat """
                    if not exist build\\jar mkdir build\\jar
                    cd build\\classes
                    "%JAVA_HOME%\\bin\\jar" cvmf MANIFEST.MF ..\\jar\\MyApplication.jar *
                """
            }
        }

        stage('Run') {
            steps {
                bat """
                    "%JAVA_HOME%\\bin\\java" -jar build\\jar\\MyApplication.jar 10 + 5
                """
            }
        }
    }
}
