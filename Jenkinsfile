pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git url: 'https://github.com/cvmanasa/Banking-java-project/'
                 echo 'github url checkout'
            }
        }
        stage('HTML Report'){
            steps{
                echo 'Generating HTML Report'
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Banking/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
            }
        }
        stage('codecompile'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('code package'){
            steps{
                sh 'mvn package'
            }
        }
        stage('build docker image'){
          steps{
               sh 'docker build -t manasabanking .'
           }
         }
        stage('push dockerhub'){
            withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
        // some block
        }
            sh 'docker login -u cvmanasa -p ${dockerhub}'
        }
        stage('port expose'){
            steps{
                sh 'docker run -dt -p 8091:8091 --name c000 myimg'
            }
        }   
    }
}
