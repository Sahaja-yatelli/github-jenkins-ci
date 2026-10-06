# GitHub Integration with Jenkins for Continuous Integration

## Project Overview
This project demonstrates Continuous Integration using GitHub and Jenkins.
Whenever source code is pushed to GitHub, Jenkins can automatically fetch the
latest code, build the Maven project, run JUnit tests, and publish the test result.

## Technology Stack
- Java 17
- Maven
- JUnit 5
- Git
- GitHub
- Jenkins

## Project Flow
Developer -> GitHub -> Webhook -> Jenkins -> Maven Build/Test -> JUnit Report

## Local Run

Prerequisites:
- JDK 17+
- Maven 3.9+
- Git

Run:
```bash
mvn clean test
```

Expected result:
```text
Tests run: 3, Failures: 0, Errors: 0
BUILD SUCCESS
```

## GitHub Setup
1. Create a GitHub repository named `github-jenkins-ci`.
2. Push this project to the repository.
3. In Jenkins, create a Pipeline job.
4. Select "Pipeline script from SCM".
5. Select Git and enter your GitHub repository URL.
6. Set branch to `*/main`.
7. Jenkins will read the `Jenkinsfile` from the repository.

## Jenkins Setup
Make sure Jenkins has:
- Git plugin
- Pipeline plugin
- JUnit plugin
- Maven integration/support
- JDK 17 configured as `JDK17`
- Maven configured as `Maven`

For a Windows Jenkins agent, the Jenkinsfile uses:
```text
mvn clean test
```

If your Jenkins agent is Linux, replace the `bat` command in the Jenkinsfile with:
```groovy
sh 'mvn clean test'
```

## GitHub Webhook
In GitHub:
Repository -> Settings -> Webhooks -> Add webhook

Payload URL:
```text
http://YOUR-JENKINS-SERVER/github-webhook/
```

Content type:
`application/json`

Event:
`Just the push event`

In Jenkins, enable:
`GitHub hook trigger for GITScm polling`

Note: GitHub must be able to reach the Jenkins webhook URL. A Jenkins instance available only at localhost cannot receive GitHub's webhook directly.

## Demo
1. Push the project to GitHub.
2. Trigger the Jenkins pipeline.
3. Jenkins checks out the repository.
4. Maven compiles and tests the project.
5. JUnit results are published.
6. Jenkins shows SUCCESS or FAILURE.

To demonstrate failure, temporarily change the expected value in
`CalculatorTest.java`, push the change, and run the pipeline again.
Jenkins should report a failed test. Restore the correct value and push again.

## Project Modules
1. Source Code Management
2. GitHub Repository
3. Jenkins Pipeline
4. Automated Build
5. Automated Testing
6. Test Reporting
7. Webhook-based CI Trigger

## Outcome
The project demonstrates how Continuous Integration reduces manual build/test
work and provides rapid feedback whenever code changes are pushed.
