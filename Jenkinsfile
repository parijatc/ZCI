node {

    stage('Checkout') {

        // Checkout files.
        checkout([
            $class: 'GitSCM',
            branches: [[name: '*/master']],
            doGenerateSubmoduleConfigurations: false,
            extensions: [], submoduleCfg: [],
            userRemoteConfigs: [[
                credentialsId: '075e374f-41fa-49aa-80da-d3d613769036',
                url: 'https://github.com/parijatc/ZCI.git'
            ]]
        ])
    }

    stage('build') {
        // Build and Test
        sh 'xcodebuild -scheme "JenkinsTesting" -configuration "Debug" build test -destination "platform=iOS Simulator,name=iPhone 8,OS=11.2" -enableCodeCoverage YES | /usr/local/bin/xcpretty -r junit'
    }
    stage('fastlane') {
    sh 'whereis fastlane'

    dir ('/Users/Shared/Jenkins/Downloads/ZCI') {
    fastlane("beta")
    }
    //sh 'fastlane("beta")'
    }

    stage('post-build') {
        // Publish test restults.
        step([$class: 'JUnitResultArchiver', allowEmptyResults: true, testResults: 'build/reports/junit.xml'])
    }

    stage('archive') {
        //Archiving artifacts
        archiveArtifacts '**'
    }

}
