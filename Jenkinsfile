node {
  env.NODEJS_HOME = "${tool 'server-js'}"
  env.PATH="${env.NODEJS_HOME}/bin:${env.PATH}"
  try {
      parallel js: {
        stage('Compress js') {
          sh '''#!/bin/bash
                for file in $(ls www/js)
                do
                  uglifyjs www/js/$file -c -o www/min/$file
                done
          '''
        }
      },
        compress: {
          stage('Compress css') {
            sh '''#!/bin/bash
                  for file in $(ls www/css)
                  do
                    cleancss -o www/min/$file www/css/$file
                  done
            '''
          }
        }
    stage('Archiving result') {
      sh 'tar -czvf site.tar.gz www'
    }
  } finally {
      archiveArtifacts artifacts: 'site.tar.gz', onlyIfSuccessful: true
  }
}
