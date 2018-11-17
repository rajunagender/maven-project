pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '107.21.82.136', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '54.146.140.161', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "winscp -i /home/jenkins/tomcat-demo.pem **/target/*.war'
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sath "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war'
                    }
                }
            }
        }
    }
}