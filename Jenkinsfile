pipeline {
    agent any
    stages {
        stage('Clean Package'){
            steps{
                sh 'mvn clean package -DskipTests'
                // stash includes: 'target/*', name: 'target'
            }
        }

        stage('Unit tests + SonarQube Scan') {
            steps{
                script{ 
                    withSonarQubeEnv('SonarQubeServer10') {
                        withCredentials([string(credentialsId: 'developer01-token', variable: 'TOKEN')]) { 
                            sh "mvn verify sonar:sonar -Dsonar.login=$TOKEN "
                        }
                        
                    }
                }
            }
        }
        stage("SonarQube Quality Gate") {
            steps {
                sleep(180)
                script {
                    timeout(time: 10, unit: 'MINUTES') {
                        def qg = waitForQualityGate()
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}


        // stage('Unit tests + SonarQube Scan') {
        //     steps{
        //         script{
        //             withSonarQubeEnv('SonarQubeServer') {
        //                 withCredentials([string(credentialsId: 'developer01-token', variable: 'TOKEN')]) { //set SECRET with the credential content
        //                     // sh "mvn verify sonar:sonar -Dsonar.login=${TOKEN}"
        //                     sh "mvn verify sonar:sonar -Dsonar.login=b1637ad391792e6224afc867bb75c5dbf06417bb"
                            
        //                 }
                        
        //             }
        //         }
        //     }  
        // }

