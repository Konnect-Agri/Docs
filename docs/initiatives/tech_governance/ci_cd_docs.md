---
sidebar_position: 3
sidebar_label: CI/CD Pipeline
---
# Continuous Integration & Deployment
---
### What is CI/CD? 

Continuous integration (CI) and continuous delivery (CD), also known as CI/CD, embodies a culture, operating principles, and a set of practices that application development teams use to deliver code changes more frequently and reliably.

CI/CD is a best practice for devops teams. It is also a best practice in agile methodology. By automating integration and delivery, CI/CD lets software development teams focus on meeting business requirements while ensuring code quality and software security.

## CI/CD defined
Continuous integration is a coding philosophy and set of practices that drive development teams to frequently implement small code changes and check them in to a version control repository. Most modern applications require developing code using a variety of platforms and tools, so teams need a consistent mechanism to integrate and validate changes. Continuous integration establishes an automated way to build, package, and test their applications. Having a consistent integration process encourages developers to commit code changes more frequently, which leads to better collaboration and code quality.

Continuous delivery picks up where continuous integration ends, and automates application delivery to selected environments, including production, development, and testing environments. Continuous delivery is an automated way to push code changes to these environments.


## Automating the CI/CD pipeline
CI/CD tools help store the environment-specific parameters that must be packaged with each delivery. CI/CD automation then makes any necessary service calls to web servers, databases, and other services that need restarting. It can also execute other procedures following deployment.

Because the objective is to deliver quality code and applications, CI/CD also requires continuous testing. In continuous testing, a set of automated regression, performance, and other tests are executed in the CI/CD pipeline.

A mature devops team with a robust CI/CD pipeline can also implement continuous deployment, where application changes run through the CI/CD pipeline and passing builds are deployed directly to the production environment. Some teams practicing continuous deployment elect to deploy daily or even hourly to production, though continuous deployment isn’t optimal for every business application.

Organizations that implement a CI/CD pipeline often have several devops best practices in place, including microservices development, serverless architecture, continuous testing, infrastructure as code, and deployment containers. Each of these practices improves process automation and increases the robustness of cloud computing environments. Together, these practices provide a strong foundation to support continuous deployment.

## How continuous integration improves collaboration and code quality
Continuous integration is a development philosophy backed by process mechanics and automation. When practicing continuous integration, developers commit their code into the version control repository frequently; most teams have a standard of committing code at least daily. The rationale is that it’s easier to identify defects and other software quality issues on smaller code differentials than on larger ones developed over an extensive period. In addition, when developers work on shorter commit cycles, it is less likely that multiple developers will edit the same code and require a merge when committing.

Teams implementing continuous integration often start with the version control configuration and practice definitions. Although checking in code is done frequently, agile teams develop features and fixes on shorter and longer timeframes. Development teams practicing continuous integration use different techniques to control what features and code are ready for production.

Many teams use feature flags, a configuration mechanism to turn features and code on or off at runtime. Features that are still under development are wrapped with feature flags in the code, deployed with the main branch to production, and turned off until they are ready to be used. In recent research, devops teams using feature flags had a ninefold increase in development frequency. Feature flagging tools such as CloudBees, Optimizely Rollouts, and LaunchDarkly integrate with CI/CD tools to support feature-level configurations.

## Automated builds
In an automated build process, all the software, database, and other components are packaged together. For example, if you were developing a Java application, continuous integration would package all the static web server files such as HTML, CSS, and JavaScript along with the Java application and any database scripts.

Continuous integration not only packages all the software and database components, but the automation will also execute unit tests and other types of tests. Testing provides vital feedback to developers that their code changes didn’t break anything.

Most CI/CD tools let developers kick off builds on demand, triggered by code commits in the version control repository, or on a defined schedule. Teams need to determine the build schedule that works best for the size of the team, the number of daily commits expected, and other application considerations. A best practice is to ensure that commits and builds are fast; otherwise, these processes may impede teams trying to code quickly and commit frequently.



## Stages in the continuous delivery pipeline
Continuous delivery is the automation that pushes applications to one or more delivery environments. Development teams typically have several environments to stage application changes for testing and review. A devops engineer uses a CI/CD tool such as Jenkins, CircleCI, AWS CodeBuild, Azure DevOps, Atlassian Bamboo, Argo CD, Buddy, Drone, or Travis CI to automate the steps and provide reporting.

For example, Jenkins users define their pipelines in a Jenkinsfile that describes different stages such as build, test, and deploy. Environment variables, options, secret keys, certifications, and other parameters are declared in the file and then referenced in stages. The post section handles error conditions and notifications.

A typical continuous delivery pipeline has build, test, and deploy stages. The following activities could be included at different stages:

Pulling code from version control and executing a build.
Enabling stage gates for automated security, quality, and compliance checks and supporting approvals when required.
Executing any required infrastructure steps automated as code to stand up or tear down cloud infrastructure.
Moving code to the target computing environment.
Managing environment variables and configuring them for the target environment.
Pushing application components to their appropriate services, such as web servers, APIs, and database services.
Executing any steps required to restart services or call service endpoints needed for new code pushes.
Executing continuous tests and rollback environments if tests fail.
Providing log data and alerts on the state of the delivery.
Updating configuration management databases and sending alerts to IT service management workflows on completed deployments.
A more sophisticated continuous delivery pipeline might have additional steps such as synchronizing data, archiving information resources, or patching applications and libraries.

Teams using continuous deployment to deliver to production may use different cutover practices to minimize downtime and manage deployment risks. One option is configuring canary deployments with an orchestrated shift of traffic usage from the older software version to the newer one. 


## CI/CD tools and plugins
CI/CD tools typically support a marketplace of plugins. For example, Jenkins lists more than 1,800 plugins that support integration with third-party platforms, user interface, administration, source code management, and build management.

Once the development team has selected a CI/CD tool, it must ensure that all environment variables are configured outside the application. CI/CD tools allow development teams to set these variables, mask variables such as passwords and account keys, and configure them at the time of deployment for the target environment.

Continuous delivery tools also provide dashboard and reporting functions, which are enhanced when devops teams implement observable CI/CD pipelines. Developers are alerted if a build or delivery fails. The dashboard and reporting functions integrate with version control and agile tools to help developers determine what code changes and user stories made up the build.