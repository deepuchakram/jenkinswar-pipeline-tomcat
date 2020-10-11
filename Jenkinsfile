node{

   def tomcatWeb = 'C:\\Auto_deployment\\apache-tomcat-8.5.58\\webapps'
   def tomcatBin = 'C:\\Auto_deployment\\apache-tomcat-8.5.58\\apache-tomcat-8.5.58\\bin'
   def tomcatStatus = ''
   stage('SCM Checkout'){
     git 'https://github.com/deepuchakram/jenkinswar-pipeline-tomcat.git'
   }
   stage('Compile-Package-create-war-file'){
      // Get maven home path
      def mvnHome =  tool name: 'maven', type: 'maven'   
      bat "${mvnHome}/bin/mvn package"
      }
/*   stage ('Stop Tomcat Server') {
               bat ''' @ECHO OFF
               wmic process list brief | find /i "tomcat" > NUL
               IF ERRORLEVEL 1 (
                    echo  Stopped
               ) ELSE (
               echo running
                  "${tomcatBin}\\shutdown.bat"
                  sleep(time:10,unit:"SECONDS") 
               )
'''
   }*/
   stage('Deploy to Tomcat'){
     bat "copy target\\JenkinsWar.war \"${tomcatWeb}\\JenkinsWar.war\""
   }
      stage ('Start Tomcat Server') {
         sleep(time:5,unit:"SECONDS") 
         bat "${tomcatBin}\\startup.bat"
         sleep(time:100,unit:"SECONDS")
   }
}
