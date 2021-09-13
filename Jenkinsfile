

properties([
    parameters([
        fileParam(name: 'testplan.jmx'),
        fileParam(name: 'users.csv'),
        booleanParam(name: 'doClean', defaultValue: true, description: 'Clean Ws'),
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
            // sh "wget https://raw.githubusercontent.com/Blazemeter/taurus/master/examples/jmeter/stepping.yml"
    }
    
    stage("run test") {
        bzt "${workspace}/existing_jmeter_script.yml"
    }
}