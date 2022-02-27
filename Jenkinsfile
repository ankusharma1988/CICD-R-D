pipeline {
  agent any
  options {
        timeout(time: 4, unit: 'HOURS') 
    }   
  environment {
    APPSYSID = '5a90f48f1b318110089dc9961a4bcb03'
    CREDENTIALS = 'servicenow'
    DEVENV = 'https://hcltechdemosls4.service-now.com'
    PRODENV = 'https://ven03869.service-now.com'
    TESTSUITEID = 'bf8c266d732333005ce769972bf6a777'
  }
    

stages {
    stage('Build') {
      steps {
        snApplyChanges(appSysId: "${APPSYSID}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", appSysId: "${APPSYSID}",
          isAppCustomization: true, obtainVersionAutomatically: true, incrementBy: 2)
          
       
        
      }
    }
  
  
  stage('Test'){
           steps {
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
        
        
      }
    }
    
    
    stage('Install'){
           steps {
        snDevOpsChange()
       snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}", baseAppAutoUpgrade: false)
        
        
      }
    }


}

}
