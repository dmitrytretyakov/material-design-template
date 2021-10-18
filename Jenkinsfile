pipeline {
  agent any
  stages {
    stage('Parallel compressins js and css') {
      parallel {
        stage('Compress js') {
          steps {
            nodejs(nodeJSInstallationName: 'server-js') {
              sh '''#!/bin/bash
                    for file in $(ls www/css)
                    do
                      uglifyjs www/css/$file -c -o www/min/$file
                      cat www/min/$file
                    done
              '''
            }
          }
        }
      }
    }
  }
}
