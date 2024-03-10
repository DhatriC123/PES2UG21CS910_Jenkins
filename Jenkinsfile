pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Compile the .cpp file
                    sh 'g++ -o YOUR_SRN-1 your_cpp_file.cpp'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run the compiled executable
                    sh './YOUR_SRN-1'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Create a new working .cpp file
                    writeFile file: 'new_cpp_file.cpp', text: '#include <iostream>\n\nint main() {\n    std::cout << "Hello, World!" << std::endl;\n    return 0;\n}'

                    // Commit and push the new file to the repository
                    sh 'git config --global user.email "you@example.com"'
                    sh 'git config --global user.name "Your Name"'
                    sh 'git add new_cpp_file.cpp'
                    sh 'git commit -m "Add new_cpp_file.cpp"'
                    sh 'git push <your_repo_url> master'
                }
            }
        }
    }

    post {
        always {
            // Display 'pipeline failed' in case of any errors within the pipeline
            echo "Pipeline ${currentBuild.result}"
            if (currentBuild.resultIsBetterOrEqualTo('FAILURE')) {
                echo "Pipeline failed"
            }
        }
    }
}
