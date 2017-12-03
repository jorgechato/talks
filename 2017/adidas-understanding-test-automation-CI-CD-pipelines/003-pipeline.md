## The Pipeline
notes:
The main idea behind the Pipelines is to go from develop to production.

It is a file or snippet written in groovy.

The are different components on it, we are going to cover most of
them.

/---/
![](2017/images/adidas-understanding-test-automation-CI-CD-pipelines/node.jpg)
```groovy
node ("docker") {
	....
}
```
> The Nodes
notes:
The agent is the machine or VM where our project is going to be executed

You can specify the node by the agent name or the labels

/---/
![](2017/images/adidas-understanding-test-automation-CI-CD-pipelines/stages.jpg)
```groovy
stage('Checkout & Setup libs') {
	....
}
```
> The Stages

/---/
```groovy
try {
	....
} catch (def e) {
	println e
	currentBuild.result = 'FAILURE'
} finally {
	....
}
```
> The Errors

/---/
```groovy
retry(3){
	....
}
```
> Bonus

/---/
```groovy
#!/usr/bin/env groovy

// project config
def commit
def branch

// git config
def gitCredentials = 'service_account'

@Library(['global-jenkins-library@master']) _

// pipeline
node ("docker") {
	stage('Checkout & Setup libs') {
		checkout scm
		branch = env.BRANCH_NAME

		get = load './vars/get.groovy'
		test = load './vars/test.groovy'
		report = load './vars/report.groovy'
		features = load './vars/features.groovy'

		commit = gitUtils.getCommitId()

        bitbucketUtils.notify message: "Collect info", commit: commit, status: 'progress', credentials: gitCredentials
	}

	stage('Sonar') {
		bitbucketUtils.notify message: "Sonar", commit: commit, status: 'progress', credentials: gitCredentials
		sonar.run version: '1.0', branch: branch
	}

	stage('Test') {
		try {
			sh "gradle check --continue"
			bitbucketUtils.notify commit: commit, status: 'success', credentials: gitCredentials
		} catch (def e) {
			println e
			bitbucketUtils.notify commit: commit, status: 'error', credentials: gitCredentials
			currentBuild.result = 'FAILURE'
		} finally {
			publishHTML([
					reportDir  : 'build/reports/tests/test',
					reportFiles: 'index.html',
					reportName : 'Test Report',
					reportTitles: '',
					allowMissing: true,
					alwaysLinkToLastBuild: true,
					keepAll: true,
			])
		}
	}

	if (env.BRANCH_NAME == 'master') {
		stage('Doc') {
			sh "gradle groovydoc"

			publishHTML([
					reportDir  : 'docs',
					reportFiles: 'index-all.html',
					reportName : 'Documentation',
					reportTitles: '',
					allowMissing: true,
					alwaysLinkToLastBuild: true,
					keepAll: true,
			])
		}
	}
}
```
> The Real Power
