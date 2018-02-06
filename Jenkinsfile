node {

    stage('Checkout/Build') {

        // Checkout files.
        checkout([
            $class: 'GitSCM',
            branches: [[name: '*/master']],
            doGenerateSubmoduleConfigurations: false,
            extensions: [], submoduleCfg: [],
            userRemoteConfigs: [[
                credentialsId: '075e374f-41fa-49aa-80da-d3d613769036',
                url: 'http://MohdAleem@scmci.noncd.rz.db.de/bitbucket/scm/zcit/z_citest.git'
            ]]
        ])
        
        // build job: 'z_citest', parameters: [string(name: 'JenkinsTesting', value: 'JenkinsTesting')]

                // Build and Test
        sh 'xcodebuild -scheme "JenkinsTesting" -configuration "Debug" build test -destination "platform=iOS Simulator,name=iPhone 8,OS=11.2" -enableCodeCoverage YES | /usr/local/bin/xcpretty -r junit'
        
                // Publish test restults.
        step([$class: 'JUnitResultArchiver', allowEmptyResults: true, testResults: 'build/reports/junit.xml'])
        
        //Archiving artifacts
        archiveArtifacts '**'
    }
}