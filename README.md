# Branching model

![Branching model](https://cdn.rawgit.com/dev-cafe/branching-model/54f2f2aa2cf7a0bece/images/branching_model.png)



## Assumptions

This branching model assumes:

* that the project uses [semantic versioning](http://semver.org)
* that the project strictly adheres to a fork-and-pull-request (or fork-and-merge-request) workflow

This branching model can ensure that the proper definition of bugfixes and new
features is enforced.


## Branch semantics

1. `master` gathers work towards the next **major** release.
2. `release` branches are minted from `master` when a new **major** release is ready.
3. `release/X.Y.Z` branches collect all **patch** releases to a given X.Y
   release series.
4. In each **minor** series, i.e. `release/1.0.Z`, **no new features** are
   added, only bugfixes. Each new bugfix requires a bump in **patch** number,
   signalled by _tagging_
5. Important bugfixes in a given `release/X.Y.Z` can, if necessary, be ported
   to `master` by _cherry picking_ (the porting needs clarification)
6. Important bugfixes in `master` can, if necessary, be ported to
   `release/X.Y.Z` by _cherry picking_ (the porting needs clarification)
7. When a new **major** and/or **minor** release is minted, i.e. the
   corresponding branch is created, support for previous versions can be
   dropped. Bugfixes to previous versions are only released if a suitable PR
   addresses them.


## Pull requests (PRs)

1. PRs from any fork should __never__ start from the branch to which they are
   directed in the upstream repository.
   This is why this is a [good idea](http://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/).
   Example: to submit a PR towards `release/1.0.Z` fixing issue 137,
   fork the repository, and in the fork
   create a branch `release/1.0.Z-issue-137` from `release/1.0.Z`
   and submit PR towards the upstream `release/1.0.Z`.
2. **Bugfix PRs** are directed towards the relevant `release/X.Y.Z` upstream branch.
3. **API-breaking feature PRs** are directed towards the `master` upstream branch.
4. **API-preserving feature PRs** can be directed either to `master` or to the corresponding release branch and then ported to `master`.

_Images served thanks to [rawgit.com](https://rawgit.com)_.
