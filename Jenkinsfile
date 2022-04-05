pipeline {
    // 스테이지 별로 다른 거
    agent any

    triggers {
        pollSCM('*/3 * * * *')
    }

    stages {
        // 레포지토리를 다운로드 받음
        stage('Prepare') {
            agent any
            
            steps {
                echo 'Clonning Repository'

                git url: 'https://github.com/gyus13/temp.git',
                    branch: 'main'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    echo 'Successfully Cloned Repository'
                }

                always {
                  echo "i tried..."
                }

                cleanup {
                  echo "after all other post condition"
                }
            }
        }
        
        // stage('Lint Backend') {
        //     // Docker plugin and Docker Pipeline 두개를 깔아야 사용가능!
        //     agent {
        //       docker {
        //         image 'node:16'
        //       }
        //     }

        //     steps {
        //       dir ('./server'){
        //           sh '''
        //           npm install&&
        //           npm run lint
        //           '''
        //       }
        //     }
        // }

        // stage('Test Backend') {
        //   agent {
        //     docker {
        //       image 'node:16'
        //     }
        //   }
        //   steps {
        //     echo 'Test Backend'

        //     dir ('./server'){
        //         sh '''
        //         npm install
        //         npm run test
        //         '''
        //     }
        //   }
        // }
        
        stage('Bulid Backend') {
          agent any
          steps {
            echo 'Build Backend'

            dir ('./server'){
                sh """
                docker image build -t gyus13/temp:latest .
                """
            }
          }

          post {
            failure {
              error 'This pipeline stops here...'
            }
          }
        }
        

        // stage('Push Image') {
        
        // 			steps {
        // 				sh 'docker push gyus13/temp:latest'
        // 			}
        // 		}
    }
}