pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "git update-index --chmod=+x gradlew"
                    sh "./gradlew compileJava"
               }
          }
          stage("Unit test") {
               steps {
                    sh "./gradlew test"
               }
          }
     }
}