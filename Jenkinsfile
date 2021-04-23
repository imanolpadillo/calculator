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
               subject: "test1",
               body: "body"
          }
     }
}