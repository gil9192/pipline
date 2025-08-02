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
                    cat build/computer.txt
                    sleep 600
                    echo "Display" >> build/computer.txt
                    cat build/computer.txt
                    echo "Keyboard" >> build/computer.txt
                    cat build/computer.txt
                '''
            }
        }
    }
    
    post {
        success {
            echo 'Build completed successfully!'
            archiveArtifacts artifacts: 'build/**' 
        }
        // failure {
        //     echo 'Build failed!'
        // }
    }
}
