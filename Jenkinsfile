properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Unit Tests'){
        git 'https://github.com/jnghn1/java-project.git'
        sh "ant"
    }
    
    stage('Build'){
        sh "ant"
    }
    
    stage('Deploy'){
        sh "ant"
    }
    
    stage('Reports'){
        junit 'reports/*.xml'
    }
}
