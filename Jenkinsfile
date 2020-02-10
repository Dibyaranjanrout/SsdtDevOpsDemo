try{
node ('winazureagent1'){

    ws('D:\\workspace\\CDS_SQL') {
    stage('Checkout')
    {
        git branch: 'master', git credentialsId: '7dd87e18-c6a1-4c87-babe-7f756acd6936' ,url: 'https://github.com/Dibyaranjanrout/SsdtDevOpsDemo.git'
        
    }
    
    stage('Build Dacpac from SQLProj') {
        
        bat "\"${tool name: 'Default', type: 'msbuild'}\" /p:Configuration=Release"
        stash includes: 'SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac', name: 'theDacpac'
    }
 
    stage('Deploy Dacpac to SQL Server') {
        unstash 'theDacpac'
        bat "\"C:\\Program Files (x86)\\Microsoft SQL Server\\130\\DAC\\bin\\sqlpackage.exe\" /Action:Publish /SourceFile:\"SsdtDevOpsDemo\\bin\\Release\\SsdtDevOpsDemo.dacpac\" /TargetServerName:(local) /TargetDatabaseName:Chinook"
    }
}
}
}

catch(Exception err) {  
        stage('Error Info'){
         echo "Something went wrong"
         echo err
            
        }
		
    
    currentBuild.result = 'FAILURE'    
    }
