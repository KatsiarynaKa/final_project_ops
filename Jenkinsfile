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
               bat 'echo Main-Class: Calculator > MANIFEST.MF'
            }
        }
        
        stage('Package') {
            steps {
            bat packageCommand = "jar cvmf MANIFEST.MF Calculator.jar -C build ."
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/Calculator.jar', allowEmptyArchive: true
            }
        }

        stage('increment version') {
        steps {
            script {
                echo 'incrementing app version...'
                bat 'mvn build-helper:parse-version versions:set \
                    -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                    versions:commit'
                def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                def version = matcher[0][1]
                env.IMAGE_NAME = "$version-$BUILD_NUMBER"
            }
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

