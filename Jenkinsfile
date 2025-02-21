// pipeline {
//     agent any

//     stages {
        
//         stage('Restore Dependencies') {
//             steps {
//                 sh 'dotnet restore'
//             }
//         }

//         stage('Build') {
//             steps {
//                 sh 'dotnet build --no-restore'
//             }
//         }

//         stage('Run Tests') {
//             steps {
//                 sh 'dotnet test --no-build --verbosity normal'
//             }
//         }
//     }
// }

pipeline {
    agent any

    stages {
        stage('Verify Workspace') {
            steps {
                sh 'pwd'  // Print current directory
                sh 'ls -lah'  // Show all files
                sh 'git rev-parse --is-inside-work-tree'
            }
        }

        stage('Force Git Directory') {
            steps {
                script {
                    dir('SUContent-SEDO-Regular-Exam-2024-10-2') {
                        sh 'pwd'  // Debug: Print working directory
                        sh 'git rev-parse --is-inside-work-tree'
                        sh 'git status'
                    }
                }
            }
        }

        stage('Restore Dependencies') {
            steps {
                script {
                    dir('HomiesProject') {  // Run in the correct directory!
                        sh 'dotnet restore Homies.sln'  // Specify the solution file
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    dir('HomiesProject') {
                        sh 'dotnet build Homies.sln --no-restore'
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    dir('HomiesProject') {
                        sh 'dotnet test Homies.sln --no-build --verbosity normal'
                    }
                }
            }
        }
    }
}
