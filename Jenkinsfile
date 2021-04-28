pipeline {
     agent any
     triggers {
          pollSCM('* * * * *')
     }
     stages {
          stage("Compile") {
               steps {
                    sh "chmod +x gradlew"
                    sh "./gradlew compileJava"
               }
          }
          stage("Unit test") {
               steps {
                    sh "./gradlew test"
               }
          }
          stage("Package") {
               steps {
                    sh "./gradlew build"
               }
          }
          stage("Docker build") {
               steps {
                    sh "chmod +x /var/run/docker.sock"
                    sh "chmod +x /usr/local/bin/docker"
                    sh "docker build -t imanolpadillo/calculator ."
               }
          }
          stage("Docker push") {
               steps {
                    sh "docker push imanolpadillo/calculator"
               }
          }
          stage("Code coverage") {
               steps {
                    echo "./gradlew jacocoTestReport"
                    echo "./gradlew jacocoTestCoverageVerification"
               }
          }
          stage("Static code analysis") {
               steps {
                    sh "./gradlew checkstyleMain"
                    publishHTML (target:[
                         reportDir: 'build/reports/checkstyle/',
                         reportFiles: 'main.html',
                         reportName: "Checkstyle Report"
                    ])
               }
          }
     }
     post {
          always {
               mail to: 'useincaseoffire@gmail.com',
               subject: "Completed pipeline: ${currentBuild.fullDisplayName}",
               body: "Your build completed, please check: ${env.BUILD_URL}"
          }
     }
}