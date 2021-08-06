node {
  stage('SCM Checkout'){ 
    git url: 'https://github.com/awesomeDinesh/my-app', branch: 'main'
  }
  stage('Compile-Package'){
    def mvnHome = tool name: 'maven-3', type: 'maven'
    sh "$mvnHome/bin/mvn package"    
  }
  stage('Email Notifications'){
    mail bcc: '', 
    body: '''Hello Dinesh,
             This mail is to remind you that blah blah blah...
             Thanks''', 
    cc: '', from: '', replyTo: '', subject: 'Regarding Jenkins', to: 'thedineshshinde@gmail.com'
  }  
}
