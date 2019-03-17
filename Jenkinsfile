/*
 * Jenkinsfile
 * ldgmini/bundler
 *
 * Ensures Bundler is installed and working correctly.
 */

node {
    stage("📦 Bundler") {
        sh "gem list bundler"
        sh "which bundle"
        sh "bundle --version"
    }
}
