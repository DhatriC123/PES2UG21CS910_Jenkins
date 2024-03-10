pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    // Assume 'YOUR_SRN' is a placeholder for your actual project name
                    def projectName = 'YOUR_SRN'
                    def cppFileName = 'your_cpp_file.cpp'
                    def compileCommand = "g++ -o ${projectName} ${cppFileName}"
                    
                    // Compile the .cpp file using a shell script
                    sh script: compileCommand, returnStatus: true

                    // Check if the compilation was successful
                    if (currentBuild.resultIsBetterOrEqualTo('FAILURE')) {
                        error "Build failed: Compilation error"
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Assume 'YOUR_SRN' is a placeholder for your actual project name
                    def projectName = 'YOUR_SRN'
                    def testCommand = "./${projectName}"

                    // Print the output of the .cpp file using a shell script
                    sh script: testCommand, returnStatus: true

                    // Check if the test was successful
                    if (currentBuild.resultIsBetterOrEqualTo('FAILURE')) {
                        error "Test failed: Check your code and try again"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                // Add deployment steps here if needed
                echo "Deployment steps go here"
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
