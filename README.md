# CDK Orb
[![CircleCI Build Status](https://circleci.com/gh/myhelix/cdk-orb.svg?style=shield "CircleCI Build Status")](https://circleci.com/gh/myhelix/cdk-orb) [![CircleCI Orb Version](https://img.shields.io/badge/endpoint.svg?url=https://badges.circleci.io/orb/helix/cdk)](https://circleci.com/orbs/registry/orb/helix/cdk) [![GitHub License](https://img.shields.io/badge/license-MIT-lightgrey.svg)](https://raw.githubusercontent.com/myhelix/cdk-orb/master/LICENSE) [![CircleCI Community](https://img.shields.io/badge/community-CircleCI%20Discuss-343434.svg)](https://discuss.circleci.com/c/ecosystem/orbs)

An Orb to facilitate building, testing and running [aws-cdk](https://github.com/aws/aws-cdk) applications.

## Version notes
As we are moving to yarn as the default package manager, the latest version of the orb has yarn as the package manager, while the old version uses npm.  
To use npm be sure the orb version is less than v1.0.0, while anything at level v1.0.0 and higher will use yarn as the package manager.


Additional READMEs are available in each directory.

**Meta**: This repository is open for contributions! Feel free to open a pull request with your changes. Due to the nature of this repository, it is not built on CircleCI. The Resources and How to Contribute sections relate to an orb created with this template, rather than the template itself.

## Resources

[CircleCI Orb Registry Page](https://circleci.com/developer/orbs/orb/myhelix/cdk) - The official registry page of this orb for all versions, executors, commands, and jobs described.
[CircleCI Orb Docs](https://circleci.com/docs/2.0/orb-intro/#section=configuration) - Docs for using and creating CircleCI Orbs.

### How to Contribute

We welcome [issues](https://github.com/myhelix/cdk-orb/issues) to and [pull requests](https://github.com/myhelix/cdk-orb/pulls) against this repository!

### How to Publish
* Create and push a branch with your new features.
* When ready to publish a new production version, create a Pull Request from fore _feature branch_ to `master`.
* The title of the pull request must contain a special semver tag: `[semver:<segment>]` where `<segment>` is replaced by one of the following values.

| Increment | Description|
| ----------| -----------|
| major     | Issue a 1.0.0 incremented release|
| minor     | Issue a x.1.0 incremented release|
| patch     | Issue a x.x.1 incremented release|
| skip      | Do not issue a release|

Example: `[semver:major]`

* Squash and merge. Ensure the semver tag is preserved and entered as a part of the commit message.
* On merge, after manual approval, the orb will automatically be published to the Orb Registry.


For further questions/comments about this or other orbs, visit the Orb Category of [CircleCI Discuss](https://discuss.circleci.com/c/orbs).

