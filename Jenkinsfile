pipeline
{
    agent any
    stages
    {
        stage('continuosDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('continuosBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuosDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '5bf2b9f1-649b-4c5b-8776-d980c49383d0', path: '', url: 'http://172.31.39.149:8080')], contextPath: 'sai', war: '**/*.war'
            }
        }
        stage('continuosTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/declarativepipeline/testing.jar'
            }
        }
        stage('continuosDelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '5bf2b9f1-649b-4c5b-8776-d980c49383d0', path: '', url: 'http://172.31.47.128:8080')], contextPath: 'ram', war: '**/*.war'
            }
        }
        
    }
}
