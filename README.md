# workflows-and-templates
Structure for managing GHA workflows with reusable templates

## Objective
Find a simple workable way to have multiple workflows for testing, and have deployment workflows that are dependent on passing tests, without having the complexity of setting up environments, using templates or actions, etc.

Just keeping it simple.

## Documentation on example workflows in this repo

The workflows in this repo are:

* application-tests.yml: (reusable workflow)
* security-checks.yml: (reusable workflow)
* test-workflow.yml: Executes application-tests and security-checks simultaneously on every push, on any branch except for deploy and master.
* deploy-to-develop.yml: Executes application-tests on push (which also happens on merge), and if it passes, executes a step to deploy code to develop
* deploy-to-stage.yml: Executes application-tests and securrity-checks simultaneously on push (which also happens on merge), and if both pass, executes a step to deploy code to master

Test Workflow:  Executes both appliction-tests and security-checks on every push to a branch OTHER than develop and master.  This allows for work to be developed, issues on failing application tests to be addressed, and PRs open for review after all application-tests pass.

Deploy to Develop:  This allows for a continuous development workflow where PRs are reviewed and merged multiple times a day, but if security tests fail it does not impede ongoing feature development.  Security tests runs so that the team can be aware of security issues, bu these do not impede ongoing development.  Passing application-tests will succesfully deploy to the develop environment.

Deploy to Stage:  No security issues are allowed into the master branch, so both application-tests and security-tests must pass before code is merged into master and deployed to the staging environment.
