properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Unit Tests'){
        sh "ant -f test.xml -v"
    }
    
    stage('Build'){
        sh "ant -buildfile test.xml"
    }
    
    stage('Deploy'){
        sh "ant -buildfile test.xml"
    }
    
    stage('Reports'){
        junit 'reports/*.xml'
    }
}
