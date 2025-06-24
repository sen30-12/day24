namespace day24_1
{
    public class Jenkinsfile
    {
    }
pipeline {
 agent any
 
 stages {
	stage('clone'){
		steps {
			echo 'Cloning source code'
			git branch:'main', url: 'https://github.com/sen30-12/day24.git'
		}
	} // end clone

  } // end stages
}//end pipeline

 
	stage('restore package') {
		steps
		{
			echo 'Restore package'
			bat 'dotnet restore'
		}
	}

stage ('build') {
		steps {
			echo 'build project netcore'
			bat 'dotnet build  --configuration Release'
		}
	}
	

stage ('tests') {
		steps{
			echo 'running test...'
			bat 'dotnet test --no-build --verbosity normal'
		}
	}

	stage ('public den t thu muc')
	{
		steps{
			echo 'Publishing...'
			bat 'dotnet publish -c Release -o ./publish'
		}
	}


	stage ('Publish') {
		steps {
			echo 'public 2 runnig folder'
		//iisreset /stop // stop iis de ghi de file 
			bat 'xcopy "%WORKSPACE%\\publish" /E /Y /I /R "C:\\inetpub\\wwwroot\\day242"'
 		}
	}


	stage('Deploy to IIS') {
            steps {
                powershell '''
               
              
                Import-Module WebAdministration
                if (-not (Test-Path IIS:\\Sites\\MySite)) {
                    New-Website -Name "day24_1" -Port 81 -PhysicalPath "C:\\inetpub\\wwwroot\\day242"
                }
                '''
            }
        } // end deploy iis

    
}
