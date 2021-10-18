pipeline {
  agent any
  stages {
    stage('Parallel compressins js and css') {
      parallel {
        stage('Compress js') {
          steps {
            nodejs(nodeJSInstallationName: 'server-js') {
              sh '''#!/bin/bash
                    for file in $(ls www/js)
                    do
                      uglifyjs www/js/$file -c -o www/min/$file
                    done
              '''
            }
          }
        }
        stage('Compress css') {
          steps {
            nodejs(nodeJSInstallationName: 'server-js') {
              sh '''#!/bin/bash
                    for file in $(ls www/css)
                    do
                      cleancss -o www/min/$file www/css/$file
                    done
              '''
            }
          }
        }
      }
    }
    stage('Archiving result') {
      steps {
        sh 'tar -czvf site.tar.gz www'
      }
    }
  }
  post {
    success {
      archiveArtifacts artifacts: 'site.tar.gz'
    }
  }
}
