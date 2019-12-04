def readjson;
def wiki;
def trackers;
def som;
node 
{
     stage 'Buildandpush - Checkout') {
       checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'e71d86df-0a12-4ef9-b416-277f6818abfe', url: 'https://github.com/GandeevBoddeti/Retina.git']]]) 
	}
    stage('UnZip file')
    {
        jsonfile=unzip dir: '', glob: '', zipFile: 'Template_Deployment_Process.zip';
        readjson=readJSON file: 'Template_Deployment_Process.json';
        wiki=readjson.project.wikiHomePage;
        trackers=readjson.project.trackers;
        fileOperations([fileDeleteOperation(excludes: '', includes: 'Template_Deployment_Process.json')])
    }
    stage('Write json to the file')
    {
        writeJSON file: 'JsonSplitFolder/Wiki.json', json: wiki, pretty: 4
        writeJSON file: 'JsonSplitFolder/Trackers.json', json: trackers, pretty: 4
    }
    stage('Commit to the GitHub')
    {
	git credentialsId: 'e71d86df-0a12-4ef9-b416-277f6818abfe', url: 'https://github.com/GandeevBoddeti/Retina.git'
        sh  'git add .'
        sh 'git commit -m "Initial Commit"'
        sh 'git push -u origin master'
    }
}
