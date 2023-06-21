pipeline
{
    agent any
    stages
    {
        stage('ContiDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('ContiBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContiDeployment')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'd90a626e-0599-4755-a471-1a976e388b17', path: '', url: 'http://172.31.34.75:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
        stage('ContiDelivery')
        {
            steps
            {
                input message: 'Need Approval From DM', submitter: 'sai'
                deploy adapters: [tomcat9(credentialsId: 'd90a626e-0599-4755-a471-1a976e388b17', path: '', url: 'http://172.31.47.19:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
