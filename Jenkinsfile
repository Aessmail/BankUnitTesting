pipeline {
    agent {
		node {
			label "master"
			customWorkspace "D:\\Jenkins\\workspaces\\asp.net-example-scmpipeline"
		}
	}
    stages {
        stage('Build') {
            steps {
                bat "D:\\Jenkins\\Tools\\nuget\\nuget.exe restore"
				bat '"C:\\Program Files (x86)\\MSBuild\\12.0\\Bin\\amd64\\MSBuild.exe" Bank\\Bank.csproj'
				bat '"C:\\Program Files (x86)\\MSBuild\\12.0\\Bin\\amd64\\MSBuild.exe" BankTest\\BankTest.csproj'
            }
        }
        stage('Test') {
            steps {
				bat '"C:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\IDE\\MSTest.exe" /resultsfile:BankTestFirstRun.trx /noisolation /testcontainer:%WORKSPACE%\\BankTest\\bin\\Debug\\BankTest.dll'
				bat '"D:\\Jenkins\\Tools\\opencover\\tools\\OpenCover.Console.exe" -register:administrator -target:"C:\\Program Files (x86)\\Microsoft Visual Studio 12.0\\Common7\\IDE\\MSTest.exe" -targetargs:"/testcontainer:\\"%WORKSPACE%\\BankTest\\bin\\Debug\\BankTest.dll\\" /resultsfile:\\"%WORKSPACE%\\BankTestResults.trx\\"" -mergebyhash -skipautoprops -output:"%WORKSPACE%\\Coverage.xml" -filter:"+[Bank*]* -[BankTest]*"'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello world!' 
            }
        }
    }
	post {
       always {
           echo 'One way or another, I have finished'
       }
       success {
           echo 'I succeeeded!'
       }
       unstable {
           echo 'I am unstable :/'
       }
       failure {
           echo 'I failed :('
	   deleteDir() /* clean up our workspace */
       }
       changed {
           echo 'Things were different before...'
       }
   }

}
