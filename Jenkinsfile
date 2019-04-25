properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/jnghn1/java-project.git'
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
    }
    
    stage('Build'){
        sh 'ant -f build.xml -v'
    }    
    
    stage('Deploy'){
        build 'rectangle-${BUILD_NUMBER}.jar'
        sh 'aws s3 cp rectangle-${BUILD_NUMBER}.jar s3://jhpark1-assignment-4'
    }
}
