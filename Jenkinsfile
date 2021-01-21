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
        
        
    }
}
