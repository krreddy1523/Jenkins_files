pipeline{
    agent any
    stages{
        stage('checkout') {
            steps{
                checkout changelog: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'gitlab-opstree', url: 'https://gitlab.com/arunkundrupu/springhibernate3.git']]]
    }   }
        stage('Build') {
            steps{
                withMaven(jdk: 'Java8', maven: 'M2_HOME') {
                sh 'cd Spring3HibernateApp; mvn clean compile'
            }
    }   }
        stage('Test') {
            steps{
                withMaven(jdk: 'Java8', maven: 'M2_HOME') {
                sh 'cd Spring3HibernateApp; mvn clean test cobertura:cobertura'
                publishCoverage adapters: [coberturaAdapter('Spring3HibernateApp/target/site/cobertura/coverage.xml')], sourceFileResolver: sourceFiles('NEVER_STORE')
               }
            }
            }
        }
}

