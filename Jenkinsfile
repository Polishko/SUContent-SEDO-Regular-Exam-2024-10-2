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
                sh 'pwd'  // Confirm working directory
                sh 'ls -lah'  // List files
                sh 'git status || echo "Git repo not found!"'
                sh 'git remote -v || echo "No remote found!"'
            }
        }

        stage('Ensure Repo is Set Up') {
            steps {
                dir('HomiesJenkinsfile') {  // Make sure we are inside the correct directory
                    sh 'git remote remove origin || echo "No origin to remove"'
                    sh 'git remote add origin https://github.com/Polishko/SUContent-SEDO-Regular-Exam-2024-10-2'
                    sh 'git fetch origin'
                    sh 'git reset --hard origin/main'  // Ensure it's up to date
                }
            }
        }

        stage('Restore Dependencies') {
            steps {
                dir('HomiesJenkinsfile') {  // Ensure the correct directory
                    sh 'dotnet restore'
                }
            }
        }

        stage('Build') {
            steps {
                dir('HomiesJenkinsfile') {  // Ensure the correct directory
                    sh 'dotnet build --no-restore'
                }
            }
        }

        stage('Run Tests') {
            steps {
                dir('HomiesJenkinsfile') {  // Ensure the correct directory
                    sh 'dotnet test --no-build --verbosity normal'
                }
            }
        }
    }
}
