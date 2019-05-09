properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/jnghn1/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }

    stage('Build'){
        sh 'ant'
        sh 'ant -f build.xml -v'
    } 
    
    stage('Deploy'){
        sh 'aws s3 cp /java-pipeline/dist/rectangle-${BUILD_NUMBER}.jar s3://jhpark1-assignment-4'
    }
    
    stage('Report'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS-credentials-jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
        sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
        }        
    }      
}

