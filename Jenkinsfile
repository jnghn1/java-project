node('linux'){
  stage('unit test'){
      git 'https://github.com/jnghn1/java-project.git'
      sh 'ant -f test.xml -v'
      junit 'reports/result.xml'
  }
}
