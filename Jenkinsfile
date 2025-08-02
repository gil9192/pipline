pipeline {
    agent {
        kubernetes {
            yamlFile 'jenkins-pod.yaml'
            defaultContainer 'shell'
            retries 2
        }
    }

    environment {
        BUILD_FILE_NAME = 'laptop.txt'
    }

    stages {
        stage('Build') {
            steps {
                echo "Building New $BUILD_FILE_NAME"
                sh '''
                    mkdir -p build
                    touch build/$BUILD_FILE_NAME
                    echo "Mainboard" >> build/$BUILD_FILE_NAME
                    echo "Display" >> build/$BUILD_FILE_NAME
                    echo "Keyboard" >> build/$BUILD_FILE_NAME
                '''
            }
        }
        stage('Build W/ docker') {
            agent {
                docker {
                    image 'alpine:latest'
                }
            }
            steps {
                echo "Building New $BUILD_FILE_NAME on docker"
                sh '''
                    mkdir -p build
                    touch build/$BUILD_FILE_NAME
                    echo "Mainboard" >> build/$BUILD_FILE_NAME
                    echo "Display" >> build/$BUILD_FILE_NAME
                    echo "Keyboard" >> build/$BUILD_FILE_NAME
                    cat /etc/os-release
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing $BUILD_FILE_NAME"
                sh '''
                    test -f build/$BUILD_FILE_NAME
                    grep "Mainboard" build/$BUILD_FILE_NAME
                    grep "Display" build/$BUILD_FILE_NAME
                    grep "Keyboard" build/$BUILD_FILE_NAME
                '''
            }
        }
    }
    
    post {
        success {
            echo 'Build completed successfully!'
            archiveArtifacts artifacts: 'build/**' 
        }
        failure {
            echo 'Build failed!'
        }
    }
}
