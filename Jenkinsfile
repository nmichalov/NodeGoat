pipeline {
  agent {
    docker {
      image 'cypress/base:10'
      // image 'timbru31/java-node'
      
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'rm -rf node_modules && npm install'
      }
    }
    // stage('SCA') {
    //   steps {
    //     sh 'curl -sSL https://download.sourceclear.com/ci.sh | sh'
    //   }
    // }
    stage('Interactive') {
     steps {
         wrap([$class: 'VeracodeInteractiveBuildWrapper', location: 'host.docker.internal', port: '10010']) {
       // wrap([$class: 'VeracodeInteractiveBuildWrapper', location: 'iast-demo.nmichalov.sa.veracode.io', port: '443']) {
         sh 'curl -sSL https://s3.us-east-2.amazonaws.com/app.veracode-iast.io/iast-ci.sh | sh'
        //  sh 'npm run start:iast & wait-on http://localhost:4000'
         sh 'npm run start:iast'
         sh 'npm run test:ci'
       }
     }
    }
    //  stage('Static') {
    //    steps {
    //      sh 'rm -f upload.zip'
    //      zip zipFile: 'upload.zip', archive: false, glob: '*.js,*.json,app/**,artifacts/**,config/**'
    //      sh 'curl -O https://downloads.veracode.com/securityscan/pipeline-scan-LATEST.zip'
    //      sh 'unzip -o pipeline-scan-LATEST.zip pipeline-scan.jar'
    //              sh 'java -jar pipeline-scan.jar \
    //                  --veracode_api_id "${VERACODE_API_ID}" \
    //                  --veracode_api_key "${VERACODE_API_SECRET}" \
    //                  --project_name "NodeGoat" \
    //                  --file upload.zip \
    //                  --json_output_file="baseline.json"'
    //    }
    //  }
    stage('Deploy') {
      steps {
        sh 'echo npm package would run here...'
      }
    }
  }
}
