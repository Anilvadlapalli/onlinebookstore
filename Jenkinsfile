pipeline{
    agent any

    stages{
        stage('scm'){
            steps{
                checkout scm
            }
        }
        stage('Build') {
    steps {
        sh 'mvn clean package'
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
        stage('Deploy') {
    steps {
        deploy adapters: [
            tomcat9(
                credentialsId: 'admin1', 
                path: '', 
                url: 'http://100.25.132.67:8082/manager/text'
            )
        ], 
        contextPath: '/anil', 
        war: 'target/onlinebookstore-0.0.1-SNAPSHOT.war'  // adjust for Gradle if needed
    }
}
    }
}
