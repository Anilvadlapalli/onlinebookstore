pipeline{
    agent any

    stages{
        stage('scm'){
            steps{
                checkout scm
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'onlinebookstore', 
                        classifier: '', 
                        file: '/var/lib/jenkins/workspace/pipeline/target/onlinebookstore-0.0.1-SNAPSHOT.war', 
                        type: 'war'
                        ]
                    ], 
                        credentialsId: 'admin', 
                        groupId: 'onlinebookstore', 
                        nexusUrl: '100.25.132.67:8081', 
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: 'maven-snapshots', 
                        version: '0.0.1-SNAPSHOT'
            }
        }
        stage('deploy'){
            steps{
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'admin1', 
                        path: '', 
                        url: 'http://100.25.132.67:8082/')
                        ], 
                        contextPath: null, 
                        war: '**/*.war'
            }
        }
    }
}
