pipeline {
agent any
    tools {
        maven 'localMaven'
    }
    parameters { 
         string(name: 'tomcat_dev', defaultValue: '18.188.221.74', description: 'Staging Server')
    } 
 
    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
           }
         stage ('Deploy to Staging'){
                    steps {
                        bat "WinSCP -i C:/Users/Vijaya Danny/.ssh/tomcat-keypair.pem **/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
              }
        }
}