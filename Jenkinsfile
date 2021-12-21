pipeline {

    agent any

    stages {
        stage('Clean Package') {
            steps {
                sh 'mvn clean package -DskipTests -Dsonar.login=b1637ad391792e6224afc867bb75c5dbf06417bb'
                stash includes: 'target/*', name: 'target'
            }
        }


        // stage('Unit tests + SonarQube Scan') {
        //     steps{
        //         script{
        //             withSonarQubeEnv('SonarQubeServer') {
        //                 sh './mvnw verify sonar:sonar'
        //             }
        //         }
        //     }
        //     post {
        //         success {
        //             junit 'target/test-results/test/*.xml'
        //             echo 'Unit tests execution finished'
        //         }
        //     }
        // }

        stage('Maven Install') {
            steps {
                sh './mvnw install -DskipTests'
            }
        }


        // stage("SonarQube Quality Gate") {
        //     steps {
        //         sleep(180)
        //         script {
        //             timeout(time: 10, unit: 'MINUTES') {
        //                 def qg = waitForQualityGate()
        //                 if (qg.status != 'OK') {
        //                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
        //                 }
        //             }
        //         }
        //     }
        // }
    }
}