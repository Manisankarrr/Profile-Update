1. Webhooks:
Webhooks automatically trigger Jenkins pipelines when events occur (like a Git push).
They eliminate the need for Jenkins to constantly check for changes.

2. Artifacts:
Artifacts are the output files generated after a build, like binaries or test reports.
They are stored for later use, sharing, or deployment.
Eg: Docker build, .zip file ...

3. Caching:
Caching stores commonly used files or dependencies to avoid re-downloading them in every build.
It significantly reduces build time and improves efficiency.

4. Secrets Management:
Secrets management securely stores sensitive data like API keys or passwords in Jenkins.
It ensures credentials are hidden and not exposed in logs or code.

5. Environment Promotion:
Environment promotion moves a build from one stage (e.g., development) to another (e.g., production).
It ensures proper testing and validation before release.

6. Parallel/Matrix Jobs:
These jobs allow Jenkins to run multiple tasks simultaneously.
Useful for testing across different environments or configurations.


---------------------------------------------------------------------------------------------------------------------------------------------------

1. Webhooks
This line triggers build on a GitHub push:

#groovy Code:
triggers {
    githubPush()
}
Requires GitHub webhook set to: http://<jenkins-url>/github-webhook/
-------------
2. Secrets Management
This line injects a secret (from Jenkins credentials):

#groovy Code:
environment {
    API_KEY = credentials('my-secret-api-key')
}
--------------
3. Caching
We mimic caching by just running npm install (you’d use a persistent volume or external plugin in real builds).

#groovy Code:

sh 'npm install'
--------------
4. Artifacts
This line stores the build folder for later use:

#groovy Code:

archiveArtifacts artifacts: 'build/**', fingerprint: true
-------------
5. Environment Promotion
This stage only runs if the branch is main, simulating promotion to staging:

#groovy Code:

when {
    branch 'main'
}
steps {
    sh 'echo "Deploying..."'
}
--------------
6. Parallel/Matrix Jobs
These two jobs run in parallel, testing on Node 14 and Node 16:

#groovy Code:

parallel {
    stage('Test on Node 14') { ... }
    stage('Test on Node 16') { ... }
}
--------------


