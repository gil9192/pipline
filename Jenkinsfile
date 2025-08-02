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
                sh 'mkdir -p build'
                sh 'touch build/computer.txt'
                sh 'echo "Mainboard" >> build/computer.txt'
            }
        }
    }
}
