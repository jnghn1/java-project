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



}
