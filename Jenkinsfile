pipeline {
  agent {
        label 'Unity-Windows'
      }
  stages {
    stage('Prepare Environment') {
      steps {
        bat 'mkdir %ARTIFACTS%'
      }
    }
    // stage('Run Tests') {
    //   stages {
    //     stage('Test: EditMode') {
    //       environment {
    //         TEST_PLATFORM = 'EditMode'
    //       }
    //       steps {
    //         bat 'ci/test.bat'
    //       }
    //     }
    //     stage('Test: PlayMode') {
    //       environment {
    //         TEST_PLATFORM = 'PlayMode'
    //       }
    //       steps {
    //         bat 'ci/test.bat'
    //       }
    //     }
    //   }
    // }
    stage('Run Builds') {
      stages {
        stage('Build: WebGL') {
          environment {
            BUILD_TARGET = 'WebGL'
          }
          steps {
            bat 'ci/build.bat'
          }
        }

        stage('Build: StandaloneWindows64') {
          environment {
            BUILD_TARGET = 'StandaloneWindows64'
          }
          steps {
            bat 'ci/build.bat'
          }
        }

        stage('Build: StandaloneLinux64') {
          environment {
            BUILD_TARGET = 'StandaloneLinux64'
          }
          steps {
            bat 'ci/build.bat'
          }
        }
      }
    }
    stage('Archive Artifacts') {
      steps{
        // dir("${TEST_RESULTS}") {
        //   nunit testResultsPattern: '**'
        // }
        dir("${ARTIFACTS}") {
          archiveArtifacts artifacts: '**'
        }
      }
    }
  }
  environment {
    UNITY_PATH = 'D:\\Program Files\\Unity Editors\\2020.1.2f1\\Editor\\Unity.exe'
    BUILD_NAME = 'ExtraCreditsGameJam6'
    
    ARTIFACTS = "${WORKSPACE}\\_artifacts"
    TEST_RESULTS = "${WORKSPACE}\\_testResults"
  }
  post {
    always {
      deleteDir()
    }
  }
}