properties([parameters([choice(choices: 'main\nmaster\nfeature-1', description: 'Select branch to build', name: 'branch')])])

node {
  stage('SCM Checkout'){ 
    git url: 'https://github.com/awesomeDinesh/my-app', branch: "${params.branch}"
  }
  stage('Compile-Package'){
    def mvnHome = tool name: 'maven-3', type: 'maven'
    sh "$mvnHome/bin/mvn package"    
  }
  
  stage('SonarQube-Analysis'){
    def mvnHome = tool name: 'maven-3', type: 'maven'
    withSonarQubeEnv('sonar-8'){
    sh "$mvnHome/bin/mvn clean package sonar:sonar"    
    }
  }
  
  stage('QualityGate Status'){
    timeout(time: 1,unit: 'HOURS'){
      def qg = waitForQualityGate()
      if (qg.status != 'OK'){
        error "Pipeline aborted due to Quality Gate failed ${qg.status}"
      }
    }
  }
  
  stage('Email Notifications'){
    mail bcc: '', 
    body: '''Hello Dinesh,
             This mail is to remind you that blah blah blah...
             Thanks''', 
    cc: '', from: '', replyTo: '', subject: 'Regarding Jenkins', to: 'thedineshshinde@gmail.com'
  }  
}
