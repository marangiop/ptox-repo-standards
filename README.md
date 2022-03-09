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
              |
| &nbsp;                                          | Docker setup                                                    |
| &nbsp;                                          | [One-click deployment setup](one-click-deploy.md)               |

## More README Resources

You may find these resources useful for structuring your project's README file (edit and add your favourites!)

- [Art of Readme](https://github.com/noffle/art-of-readme)
- [A template to make good README.md](https://gist.github.com/PurpleBooth/109311bb0361f32d87a2)
- [Developer Experience: GitHub READMEs](https://betta.io/blog/2017/02/07/developer-experience-github-readmes)
- [Make a README](https://www.makeareadme.com/)

## Branches

For every repo we recommend to have: `production-branch`, `dev-branch`,` username-branch` (e.g., muen-branch, Paolo-branch). The idea is that multiple developers can work on their respective `username-branch`, and then use pull requests to merge code to the `dev-branch`.
The `production branch` is for a stable version of a given tool/library/infrastructure component, such that whenever changes in the `dev-branch` are merged to the `production-branch`, a new release is generated.

@DOM: talk about protect specific branches from push operations

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

