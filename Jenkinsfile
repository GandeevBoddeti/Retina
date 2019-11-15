def readjson;
def wiki;
def trackers;
def som;
node 
{
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
        sh  'git add .'
        sh 'git commit -m "Initial Commit"'
        sh 'git push -u origin master'
    }
}
