/*
 * Jenkinsfile
 * ldgmini/bundler
 *
 * Ensures Bundler is installed and working correctly.
 */

properties([
    // Don't trigger this job when changes are found from branch indexing.
    //overrideIndexTriggers(false),
    disableConcurrentBuilds(),
    pipelineTriggers([
        cron('H 1 * * *')
    ]),
    buildDiscarder(logRotator(numToKeepStr: '100')),
])

timeout(time: 1, unit: 'HOURS') {
    withEnv(['LANG=en_US.UTF-8']) {
        node {
            stage("🛒 Checkout") {
                checkout scm
            }
            stage("📦 Bundler") {
                sh "gem list bundler"
                sh "which bundle"
                sh "bundle --version"
            }
        }
    }
}
