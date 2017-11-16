node('content')
{ 
timestamps
  {
     timeout(time: 7200000, unit: 'MILLISECONDS') {
String platform='File Formats';
   try
	{   
	
	def Content="";
		env.PATH = "C:\\Program Files\\Git\\mingw64\\bin;${env.PATH}"
		
		//Clone scm repository in Workspace source directory
		stage ('Checkout')   
	    { 
	    dir('Spell-Checker') 
           {
		     checkout scm
			 
			 //get the changelog by using git difference command
			 
			 String ChangeDetails = bat returnStdout: true, script: 'git diff --name-only '+env.gitlabSourceBranch+'..origin/'+env.gitlabTargetBranch
			 
			 def ChangeFiles=ChangeDetails.split('\n')
			 
			 for(int i=2;i<ChangeFiles.size();i++)
               {
			      Content+= env.WORKSPACE+"\\Spell-Checker\\"+ChangeFiles[i]+"\r\n";
               }
		    
		      if (Content) {  
                 writeFile file: env.WORKSPACE+"/cireports/content.txt", text: Content
              }
              else  {
                writeFile file: env.WORKSPACE+"/cireports/content.txt", text: "There are no filepaths found for this commit."
              }
			  
		    }
			 
		   //Checkout the ug_spellchecker from development Source
	  checkout([$class: 'GitSCM', branches: [[name: '*/development']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'ug_spellchecker']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: env.gitlabCredentialId, url: 'https://gitlab.syncfusion.com/content/ug_spellchecker.git']]])
		 
	  }
	}
	
    catch(Exception e)
    {
		currentBuild.result = 'FAILURE'
    } 

if(currentBuild.result != 'FAILURE')
{ 
	stage 'Build Source'
	try
	{
	    gitlabCommitStatus("Build")
		{
		bat 'powershell.exe -ExecutionPolicy ByPass -File '+env.WORKSPACE+"/ug_spellchecker/build.ps1 -Script "+env.WORKSPACE+"/ug_spellchecker/build.cake -Target build -Platform \""+platform+"\" -Branch "+'"'+env.gitlabSourceBranch+'"'
	 	}
    }
	 catch(Exception e) 
    {
		currentBuild.result = 'FAILURE'
    }
}	

	stage 'Delete Workspace'
	
		def files = findFiles(glob: '**/cireports/spellcheck/*.*')      
        
    if(files.size() > 0) 		
    { 		
         archiveArtifacts artifacts: 'cireports/', excludes: null 	 
    }
	    step([$class: 'WsCleanup'])	}
	    }
}
