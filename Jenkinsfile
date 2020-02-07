try{
node ('winazureagent1'){
node {
    
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
