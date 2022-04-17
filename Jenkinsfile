def JOBID='RunBztJmeter'
/*
  Remeber remove users, : click-ap.com/jenkins2020/jmeter
*/

properties([
    parameters([
        stashedFile(name: 'testplan.jmx'),
        stashedFile(name: 'users.csv'),
        booleanParam(name: 'doClean', defaultValue: true, description: 'Clean Ws'),
        stashedFile(name: 'existing_jmeter_script')
    ])
])    
// <hudson.model.FileParameterDefinition>

def doClean= Boolean.valueOf(doClean)
def runClean= doClean ? '✓':'X'

echo """
JOB_NAME(BASE): ${JOB_NAME}(${JOB_BASE_NAME}) ${JOB_URL}
-----------------------------
         Clean? (${runClean})
=============================
"""

node {
    stage("clean") {
        if (doClean) {
            cleanWs()   // requires workspace cleanup plugin to be installed
            checkout scm
        }
    }
    
    stage('get config file') {
        unstash 'testplan.jmx'
        unstash 'users.csv'
            // sh "wget https://raw.githubusercontent.com/Blazemeter/taurus/master/examples/jmeter/stepping.yml"
    }
    
    stage("run test") {
        //bzt "${workspace}/existing_jmeter_script.yml"
        unstash 'existing_jmeter_script'
        withFileParameter('existing_jmeter_script') {
            bzt "$existing_jmeter_script"
        }
    }
}
