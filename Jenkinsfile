pipeline{
    agent any
    tools {
        maven 'local maven'
    }
    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'saving....'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }    
        }

       stage('Deploy'){
            steps{
                echo 'deploying.nihao..'
                build job:'deploy-to-staging'
            }
        } 

        stage('Deploy to production'){
            steps{
                timeout(time:5,unit:'DAYS'){
                    input message:'是否部署到生产？'
                }

                build job:'deploy-to-staging'
            }
            post {
                success {
                    echo 'yes'
                    
                }
                failure {
                    echo 'no'
                }
            }    
        }
        
    }
}
