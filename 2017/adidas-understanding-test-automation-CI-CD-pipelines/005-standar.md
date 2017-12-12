## The Library's Standards

/---/
```bash
.   build.gradle
│   gradle.properties
│   Jenkinsfile
│   sonar-project.properties
├───test
│   │   TestTest.groovy
│   └───setup
│           PipelineSpockTestBase.groovy
│           PipelineTestHelper.groovy
└───vars
        features.groovy
        get.groovy
        report.groovy
        test.groovy
```

Note:
groovy is like a teen that starts to learn magic

/---/
### Test
```groovy
import com.adidas.jenkinsTesting.PipelineTest
import setup.PipelineSpockTestBase

class TestUtil extends PipelineSpockTestBase {
    private util

    private PipelineTest test

    def setup() {
        test = new PipelineTest()
        util = test.loadScriptWithoutRunning 'vars/utils.groovy'
    }

    def shouldThrowIfSomeArgumentIsMissing() {
        given:
        final Map args = [
                bar: 'bar',
                qux: 'qux'
        ]
        final List<String> required = [
                'foo',
                'bar'
        ]

        when:
        util.validateArgs args, required

        then:
        final Exception e = thrown()
        e.message == 'foo must be defined!'
    }
}
```

/---/
```groovy
stage('Checkout & Setup libs') {
	utils = load './vars/utils.groovy'
}

stage('Test') {
	try {
		sh "gradle check --continue"
	} catch (def e) {
		currentBuild.result = 'FAILURE'
	} finally {
		// Publish results
	}
}
```

Note:
You need to load the file in a variable so you can use it inside other classes
in the same library

/---/
### [Documentation](http://deheremap7628:8080/job/Lord_Master/job/gtt-jenkins-library/job/master/Documentation/)
```groovy
/**
 * Get the features from jira by the key
 *
 * @param {String} args.key - features identification in jira (REQUIRED)
 * @param {?String} args.credentials - Custom credentials
 */
void export(Map args) {
....
}
```

/---/
### son, wait for it ...

![](2017/images/adidas-understanding-test-automation-CI-CD-pipelines/legendary.gif)

# .. sonarqube

/---/
# Q&A (3)
