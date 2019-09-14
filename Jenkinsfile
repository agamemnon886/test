pipeline {
	agent any

	// Trigger build every day in 20:59 PM
	triggers {
		pollSCM '0 * * * 1'
	}

	options {
		// Maximum number of builds to keep
		buildDiscarder(logRotator(numToKeepStr: '20'))

		// Do not allow concurrent builds
		disableConcurrentBuilds()

		// Add timestamps
		timestamps()

		// Abort build after 24 hours to prevent hanging
		timeout(time: 24, unit: 'HOURS')
	}

	stages {
		// You can change "url:" or "timeout:" in this stage  or add/remove "checkout()" functions
		stage ('Check changes') {
			steps {
				retry (2) {
					checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'test_repo'], [$class: 'CheckoutOption', timeout: 20], [$class: 'CloneOption', depth: 0, noTags: false, reference: '', shallow: false, timeout: 180]], submoduleCfg: [], userRemoteConfigs: [[url: 'clone https://github.com/agamemnon886/test.git']]])
				}
			}
		}

		stage ('Preparation') {
			steps {
				echo "Preparation ${pwd()}"
			}
		}

		stage ('Build') {
			steps {
				echo "Build"
			}
		}

		stage ('Run tests') {
			steps {
				echo "testing"
			}
		}
	}
}

