pipeline {
    agent {
        kubernetes {
            yamlFile 'jenkins-pod.yaml'
            defaultContainer 'shell'
            retries 2
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building New Laptop'
                sh '''
                    mkdir -p build
                    touch build/computer.txt
                    echo "Mainboard" >> build/computer.txt
                    echo "Display" >> build/computer.txt
                    echo "Keyboard" >> build/computer.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing Laptop'
                sh '''
                    test -f build/computer.txt
                    grep "Mainboard" build/computer.txt
                    grep "Display" build/computer.txt
                    grep "Keyboard" build/computer.txt
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
