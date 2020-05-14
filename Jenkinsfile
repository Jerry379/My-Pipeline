// pipeline {
//     agent { docker 'node:6.3' }
//     stages {
//         stage('build') {
//             steps {
//                 sh 'node --version'
//             }
//         }
//     }
// }
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Deploy') {
            steps {
                retry(3) {
                    sh './jenkins/flakey-deploy.sh'
                }

                timeout(time:3, unit:'MINUTES') {
                    echo ' 脚本要在3分钟之内执行完'
                }
            }
            steps {
                timeout(time:3, unit:'MINUTES') {
                    echo '重复执行5次，总共用时不超过3分钟'
                }
            }
        }
    }
    post {
        always {
            echo 'this will always run'
        }
        success {
            echo 'this will run only if successful'
        }
        failure {
            echo 'this will run only if failed'
        }
        unstable {
            echo 'this will run only if the run was marked'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}