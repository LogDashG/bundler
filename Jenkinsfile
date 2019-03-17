#!/usr/bin/env groovy
/*
 * Jenkinsfile
 * ldgmini/bundler
 *
 * Ensures Bundler is installed and working correctly.
 */

import jenkins.model.*

def MAIL_TO = JenkinsLocationConfiguration.get().getAdminAddress()

properties([
    // Don't trigger this job when changes are found from branch indexing.
    //overrideIndexTriggers(false),
    disableConcurrentBuilds(),
    pipelineTriggers([
        cron('H 1 * * *')
    ]),
    buildDiscarder(logRotator(numToKeepStr: '100')),
])

try {
    timeout(time: 1, unit: 'HOURS') {
        withEnv(['LANG=en_US.UTF-8']) {
            node {
                stage("🛒 Checkout") {
                    checkout scm
                }
                stage("📦 Bundler") {
                    // https://jenkins.io/doc/pipeline/steps/workflow-durable-task-step/#sh-shell-script
                    sh(
                        script: "gem list bundler",
                        label: "💎 List gems"
                    )
                    sh(
                        script: "which bundle",
                        label: "❓ Which"
                    )
                    sh(
                        script: "bundle --version",
                        label: "🏃🏻‍♂️ Run bundler"
                    )
                    sh(
                        script: "false",
                        label: "⛔ Failure"
                    )
                }
            }
        }
    }
}
catch (Exception ex) {
    mail to: "${MAIL_TO}",
         subject: "[FAILURE]  💩  😵  [JENKINS] ${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - [FAILURE]!  👻  😭  ",
         body: "${env.JOB_NAME} - Build # ${env.BUILD_NUMBER} - FAILURE (${ex.message})!"
    throw ex
}
