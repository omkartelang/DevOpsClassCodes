pipeline{
    tools{
       jdk 'myjava'
       maven 'mymaven'
    }
    agent none
    stages{
        stage('Checkout'){
            agent any
            steps{
                git 'https://github.com/omkartelang/DevOpsClassCodes.git'
            }
        }
        stage('Compile'){
            agent {label 'linux_slave'}
            steps{
                git 'https://github.com/omkartelang/DevOpsClassCodes.git'
                sh 'mvn compile'
            }
        }
        stage('CodeReview'){
            agent any
            steps{
                sh 'mvn pmd:pmd'
            }
        }
        stage('UnitTest'){
            agent any
            steps{
                sh 'mvn test'
            }
        }
        stage('MetricCheck'){
            agent any
            steps{
                sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
            post{
                always{
                    cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
                }
            }
        }
        stage('Package'){
            agent any
            steps{
                sh 'mvn package'
            }
        }
    }
}
