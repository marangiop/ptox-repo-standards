# PrecisionTox Repository Standards

<img src="https://pbs.twimg.com/profile_images/1369299935951269895/DFBww-7V_400x400.jpg" height="200px">

This project contains checklists, templates and other resources to include with your repository. Whether you're starting a new repo from scratch or migrating an existing one hosted somewhere else, please include any or all of the elements suggested below as appropriate to your repo.
If you're not sure where something goes, or you don't have permission to create a repo, talk to Ralf Weber or Albert Zhou or Paolo Marangio on Slack/e-mail.

## How to use this repostory

What you should is to use this entire repository as a template for your own Github repository within the context of PrecisionTox. To do that, you would simply fork this repository (i.e. basically creating a copy of this repo) and edit as you like, starting from obviously renaming the forked repo.

## Get the Basics Right

Naming things is hard, this part is very important! Best practice: name the project after what it does rather than what it is made of. E.g. "joke telephone answering service" rather than "sinatra voice demo".

- [ ] Give your repo **a description** and **some topics** - you can set these at the very top of the web interface, before the file listings. The description should cover the purpose and scope of the project. The tags should include `vonage` as well as the technologies used and the features of the project. For example you could have tags: `python` `redis` `verify` `postgresql`.

- [ ] Every repo must have a **license**, this will be [MIT](https://opensource.org/licenses/MIT) in most cases. See also: [GitHub docs for adding a license to your repo](https://help.github.com/en/articles/adding-a-license-to-a-repository) and always choose a standard OSI-approved license.

- [ ] Use the [basic README template](basic-readme-template.md) as a starting point for your repository. Look at the [project types](#what-type-of-project) section for what else to include for your project.

### Minimum requirements for READMEs

While most of our READMEs should have some common features, different repo types have different requirements. Here is what we expect from the different types of repo.

| Library (e.g Node.js lib)                        | Demo/Tool/Infrastructure component                              | Supporting code (e.g. for blog post)          |
| ----------------------------------------------- |-----------------------------------------------------------------| --------------------------------------------- |
| [Installation instructions](write-installation-instructions.md) | [Installation instructions](write-installation-instructions.md) | Link to what this repo is supporting          |
| Detailed [usage docs](write-usage-docs.md) for all features | [Usage examples](write-usage-docs.md)                           | &nbsp;  |
| A [CONTRIBUTING](contributing-template.md) FILE | A [CONTRIBUTING](contributing-template.md) FILE                 |
| A [CODE_OF_CONDUCT](code-of-conduct-template.md) FILE | A [CODE_OF_CONDUCT](code-of-conduct-template.md) FILE           |
| &nbsp;                                          | [One-click deployment setup](one-click-deploy.md)               |

## More README Resources

You may find these resources useful for structuring your project's README file (edit and add your favourites!)

- [Art of Readme](https://github.com/noffle/art-of-readme)
- [A template to make good README.md](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
- [Developer Experience: GitHub READMEs](https://betta.io/blog/2017/02/07/developer-experience-github-readmes)
- [Make a README](https://www.makeareadme.com/)

## Monorepos vs. multi-repos

The naive approach to building different components of a data/IT infrastructure is to split the codebase into growing numbers of small repos, along the different team/project boundaries.
Here we introduce the concept of a monorepo. A monorepo is a unified codebase containing
code for multiple projects that share underlying
dependencies, data models, functionality, tooling
and processes.
The main advantage of monorepos is that there is not a strong need on versioning, because all the consumers (e.g. database and api) are directly there in the same repo. This prevents the so-called dependency (version) hell between the different components of a given data/IT infrastructure.
We therefore advise to use mono-repos wherever possible. 
More info about mono-repos can be found [here](https://ep2021.europython.eu/media/conference/slides/Agtzv5a-python-monorepos-what-why-and-how.pdf). 

## Monorepos build tools
Since standard build tools are not designed for monorepos, if you decide to structure your repo as a monorepo we suggest to use [Pants](https://www.pantsbuild.org/) as build system. 
In a nutshell, Pants sits on top of existing standard build tools, and orchestrates them for you. 


## Advanced GitHub usage
GitHub proposes a very wide range of features to help you organise your software projects and is easily extensible by third
party tools.

### Branches
We recommend organising repositories in such a way that your `main` or `production` branch is representing the latest stable version of 
your project. This branch should be complemented by another permanent branch named `dev` where code will be merged and tested
before landing into production. The usual pipeline is as followed:
- A ticket for resolving a bug or creating a new feature is registered in the issue tracker and attributed to a developer.
- The developer creates a new branch `username-featurename` derived from `dev` and do the work on that specific branch.
- When the code is ready, a new Pull Request (PR) is opened on `dev`. Note that PR can be created as draft for testing purposes.
- Another member of the group is tagged to review the code. The code is then either approved and merged in `dev` or changes are being requested.
- Once enough features have been merged into `dev`, a new PR from `dev` to `main` can be opened and once the code is merged a new
release version can be announced.
- Remember to create the patch note associated with each new release.

If you want to enforce this process on your repositories, you can protect specific branches from receiving incoming commit/push operations.
This is what you would usually do on `main` and `dev` to make sure only reviewed PR are accepted. <br>
The Settings >> Branches panel of your GitHub repository lets you set rules on how to handle each branch individually. <br>
Click the `Add rule` button and enter the name or pattern of the branch(es) you want to control. You have a very broad
range of options to select from such as `Require a pull request before merging` and `Require approvals`.

### Code Quality
There are a lot of ways to assess the quality of a software project. We propose to review the 3 mains techniques that will help you with quality control: Continuous Integration (CI), linting and security audit.
help you with quality control: Continuous Integration (CI), linting and security audit.

#### Continuous Integration
Continuous Integration is the process through which the code is tested at each new iteration in conditions that are different
from you local development environment. This not only ensures that the code works as intended but can also be ported to
other systems. <br>
The process, at its core, start with writing unit tests for your business logic and then reporting which piece of code is tested
and which isn't. One would use tools such as [`nose`](https://pypi.org/project/nose/) or [`pytest`](https://docs.pytest.org/en/7.0.x/) 
to run the tests and generate the coverage report. That process can then be exported to third party tool such as GitHub 
(see automation below) so that every PR is tested before being reviewed and merged.

#### Linting
The process of linting uses a set of predefined rules to style the code in a specific way. This is key to let developers
focus on what is important and becomes the more relevant as the numbers of developers on a project increases. <br>
In Python, the specification is called [`PEP8`](https://www.python.org/dev/peps/pep-0008/) and 
one of the tool used to read and executes these rules is [`Flake8`](https://flake8.pycqa.org/en/latest/).

#### Security Audits
Security audits are much more language and infrastructure dependant but there exist a couple of tools that can help you automate
part of the process by examining the repositories and looking for bad patterns. <br>
We suggest addressing this issue by relying on [`Codacy`](https://www.codacy.com/), a third party tool that can extend the GitHub features. It
can look for both linting issues and security risks by scanning the repositories and its dependencies and then reports
potential issues directly in your GitHub dashboard.

### Project Management
GitHub also provide a tool to help you organise task priority in a Kanban style. Head to the `Projects` tab of your
repository and click the second button in the left panel (the one not marked `Beta`). Then at the top right click `New project`,
enter a name a select the `Automated kanban with reviews` template. <br>
When creating new issues you can tag them with the project's name to make them appear in the kanban dashboard.

### Automation
GitHub Actions, introduced in late 2019, are virtual machines (limitations apply) that can be executed directly in GitHub
and automate a lot of operations. A few examples of this usage are Continuous Integration and Automated Releases and
Automated Deployment. <br>
To run an Action, head to the corresponding tab in your repo. Clicking the `New workflow` will redirect you to the 
Action marketplace where you can select pre-built actions for your use case. Feel free to reach out to us if you want to
write your own workflows or want more information.