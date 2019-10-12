# Semantic Versioning 2.0.0

https://semver.org/





Semantic Versioning is all about *releases*, not builds. This means that the version only increases after you release, this directly conflicts with the concept of published CI builds. 



When you are ready to release you simply deploy the latest built version and tag the release it was from. This practice is called **continuous delivery**. 



GitVersion will increment the *metadata* for each build so you can tell builds apart. For example `1.0.0+5` followed by `1.0.0+6`. It is important to note that build metadata *is not part of the semantic version, it is just metadata!*.

If you are using GitFlow then builds off the `develop` branch will actually *increment on every commit*. This is known in GitVersion as *continuous deployment mode*. By default `develop` builds are tagged with the `alpha` pre-release tag. This is so they are sorted higher than release branches.



### Commit messages

Adding `+semver: breaking` or `+semver: major` will cause the major version to be increased, `+semver: feature` or `+semver: minor` will bump minor and `+semver: patch` or `+semver: fix` will bump the patch.

major-version-bump-message: '\+semver:\s?(breaking|major)'
minor-version-bump-message: '\+semver:\s?(feature|minor)'
patch-version-bump-message: '\+semver:\s?(fix|patch)'
commit-message-incrementing: Enabled



### GitVersion.yml

The first is by setting the `next-version` property in the GitVersion.yml file. This property only serves as a base version.



### Branch name

If you create a branch with the version number in the branch name such as `release-1.2.0` or `hotfix/1.0.1` then GitVersion will take the version number from the branch name as a source





Releae branch tag v1.3.1,  make a change and commit, the semversion is going to be v1.3.2

ContinuousDelivery



https://gitversion.readthedocs.io/en/latest/git-branching-strategies/gitflow-examples/





```yaml
next-version: 1.0 //最高规则，直接覆盖其他规则
assembly-versioning-scheme: MajorMinorPatch
assembly-file-versioning-scheme: MajorMinorPatchTag
assembly-informational-format: '{InformationalVersion}'
mode: ContinuousDelivery
increment: Inherit
continuous-delivery-fallback-tag: ci
tag-prefix: '[vV]'
major-version-bump-message: '\+semver:\s?(breaking|major)'
minor-version-bump-message: '\+semver:\s?(feature|minor)'
patch-version-bump-message: '\+semver:\s?(fix|patch)'
no-bump-message: '\+semver:\s?(none|skip)'
legacy-semver-padding: 4
build-metadata-padding: 4
commits-since-version-source-padding: 4
commit-message-incrementing: Enabled
commit-date-format: 'yyyy-MM-dd'
ignore:
  sha: []
commits-before: yyyy-MM-ddTHH:mm:ss
branches:
	master:
	regex: master
	mode: ContinuousDelivery
	tag: ''
	increment: Patch
	prevent-increment-of-merged-branch-version: true
	track-merge-target: false
	tracks-release-branches: false
	is-release-branch: false
develop:
   regex: dev(elop)?(ment)?$
   mode: ContinuousDeployment
   tag: unstable
   increment: Minor
   prevent-increment-of-merged-branch-version: false
   track-merge-target: true
   tracks-release-branches: true
   is-release-branch: false

```



### 问题

* Develop 3.8.1 (3.8.1-alpha.6),  release/3.9.0(3.9.0-beta.2),  bugfix/4 is branched from release/3.9.0,  the gitversion in bugfix is: 3.8.1-bugfix.9
* bugfix/v3.4.1也会被识别出版本号，尽管没有被配置为release branch