# Semantic branching model

![Branching model](https://cdn.rawgit.com/dev-cafe/branching-model/54f2f2aa2cf7a0bece/images/branching_model.png)


## Assumptions for a project using the semantic branching model

* The project uses [semantic versioning](http://semver.org).
* The project strictly adheres to a fork-and-pull-request (or fork-and-merge-request) workflow.


## Goals

- Separate development towards major, minor, or patch release.
- Make it clear and simple to decide whether patches affect the next major, minor, or patch version.


## Branch semantics

1. `master` gathers work towards the next **major** release.
2. `release` branches are minted from `master` when a new **major** release is ready.
3. `release/X.Y.Z` branches collect all **patch** releases to a given X.Y
   release series.
4. In each **minor** series, i.e. `release/1.0.Z`, **no new features** are
   added, only bugfixes. Each new bugfix requires a bump in **patch** number,
   signalled by _tagging_


## Porting of changes

- Important bugfixes in a given `release/X.Y.Z` can, if necessary, be ported
  to `release/X.Y` and further to `master` by merging.
- Important bugfixes in `master` can, if necessary, be ported to `release/X.Y` and
  `release/X.Y.Z` by _cherry picking_.


## Lifetime of branches

When a new **major** and/or **minor** release branch is created,
support for previous versions can be
dropped. Bugfixes to previous versions are only released if a suitable PR
addresses them.


## Source of pull requests

A pull request (PR) PRs from any fork should never start from the branch to which they are
directed in the upstream repository.

Explanation:

- Avoid having unrelated commits stacked on top of your PR before it gets integrated
  (see also [this blogpost](http://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/)).
- The submitted changes may get rebased and/or squashed and this would create divergence and merge commits on the source branch
  which would complicate future pull requests.

Example:

- To submit a PR towards `release/1.0.Z` fixing issue 137,
  fork the repository, and in the fork
  create a branch `release/1.0.Z-issue-137` from `release/1.0.Z`
  and submit PR towards the upstream `release/1.0.Z`.


## Target of pull requests

- **Bugfix PRs** are directed towards the relevant `release/X.Y.Z` upstream branch.
- **API-breaking feature PRs** are directed towards the `master` upstream branch.
- **API-preserving feature PRs** can be directed either to `master` (then they are scheduled for the next major release)
  or to the corresponding release branch (then they are scheduled for the next minor release) and then ported to `master`.

_Images served thanks to [rawgit.com](https://rawgit.com)_.
