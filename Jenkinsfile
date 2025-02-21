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
                sh 'ls -lah'  // Show files in workspace
                sh 'git rev-parse --is-inside-work-tree || echo "Not a git repository!"'
            }
        }

        stage('Force Git Directory') {
            steps {
                script {
                    dir('SUContent-SEDO-Regular-Exam-2024-10-2') {
                        sh 'pwd'  // Print working directory
                        sh 'git rev-parse --is-inside-work-tree'
                        sh 'git status'
                    }
                }
            }
        }

        stage('Restore Dependencies') {
            steps {
                dir('SUContent-SEDO-Regular-Exam-2024-10-2') {  // Force Jenkins to use the repo directory
                    sh 'dotnet restore'
                }
            }
        }

        stage('Build') {
            steps {
                dir('SUContent-SEDO-Regular-Exam-2024-10-2') {
                    sh 'dotnet build --no-restore'
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir('SUContent-SEDO-Regular-Exam-2024-10-2') {
                    sh 'dotnet test --no-build --verbosity normal'
                }
            }
        }
    }
}
