node {
    stage("clean") {
        //cleanWs()   // requires workspace cleanup plugin to be installed
        //checkout scm
    }
    
    stage('get config file') {
            // sh "wget https://raw.githubusercontent.com/Blazemeter/taurus/master/examples/jmeter/stepping.yml"
    }
    
    stage("run test") {
        bzt "${workspace}/existing_jmeter_script.yml"
    }
}