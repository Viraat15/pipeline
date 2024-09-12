# pipeline
Scripted Syntax
===============
node
{
stage("contdownload")
     {
	    //Code
     }
}


Declarative Syntax
===================
pipeline
{
           agent any
           stages
           {
                     stage("Cont Download")
                     {
                         steps
                        {
                         //Code
                        }
                     }
           }
}


Examples: 
Scripted Example:
node
{
stage("contdownload")
     {
	 git branch: 'main', url: 'https://github.com/nocturnaldevops/Project1.git'
     }
	 stage("contbuild")
     {
	 sh 'mvn package'
     }
	 stage("contdeployment")
     {
	 deploy adapters: [tomcat9(credentialsId: 'b983fc8c-658c-4a69-8a6f-e591112c2169', path: '', url: 'http://172.31.5.27:8080')], contextPath: 'mytestapp', war: '**/*.war'
     }
	 stage("conttest")
     {
	 sh 'echo "Testing Passed"'
     }
	 stage("contdelivery")
     {
	 deploy adapters: [tomcat9(credentialsId: '91409dae-1bae-41bf-9f40-70c553c98e93', path: '', url: 'http://172.31.13.1:8080')], contextPath: 'myreleaseapp', war: '**/*.war'
     }
}
============



Declarative Example:
pipeline
{
agent any
stages
  {
      stage("contDownload")
       {
          steps
          {
          git branch: 'main', url: "https://github.com/koddas/war-web-project.git"
          }
       }
	   stage("contBuild")
       {
          steps
          {
          sh 'mvn package'
          }
       }
	   stage("contDeployment")
       {
          steps
          {
          deploy adapters: [tomcat9(credentialsId: 'b983fc8c-658c-4a69-8a6f-e591112c2169', path: '', url: 'http://172.31.5.27:8080')], contextPath: 'test01', war: '**/*.war'
          }
       }
	   stage("contTest")
       {
          steps
          {
          sh 'echo "Testing Passed"'
          }
       }
	   stage("contDelivery")
       {
          steps
          {
          deploy adapters: [tomcat9(credentialsId: '91409dae-1bae-41bf-9f40-70c553c98e93', path: '', url: 'http://172.31.13.1:8080')], contextPath: 'rel01', war: '**/*.war'
          }
       }
  }
}
