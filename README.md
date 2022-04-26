# About

GitHub action to login to AWS CodeArtifact repository.

# Usage

You need to be authenticated to AWS with user/role with proper permissions.

## Default usage

To set default mavenUser and mavenCredentials environment variables, use action
as for example here:

```yaml
name: ci

on:
  push:
    branches: main

jobs:
  login:
    runs-on: ubuntu-latest
    steps:
      - uses: aws-actions/configure-aws-credentials@v1
      - name: Login to maven
        uses: starburstdata/sep-ci-maven-login-action@v1.0.0
        with:
          domain: my-codeartifact-domain
      - name: Use credentials
        run: |
          # Make sure your maven repos user/password are set to mavenUser/mavenCredentials
          # environment variables - e.g. in ~/.m2/setttings.xml
          mvn install
```

## Input parameters

Following optional inputs can be used as `step.with` keys:

| Name                | Type   | Required | Default            | Description                                      |
|---------------------|--------|----------|--------------------|--------------------------------------------------|
| `domain`            | String | True     |                    | Name of CodeArtifact domain                      |
| `owner`             | String | False    |                    | AWS account of CodeArtifact domain               |
| `region`            | String | False    |                    | AWS region to use                                |
| `user-variable`     | String | False    | `mavenUser`        | Name of output environment variable for user     |
| `password-variable` | String | False    | `mavenCredentials` | Name of output environment variable for password |
