# branching-model-discussion

![Branching model](https://cdn.rawgit.com/robertodr/branching-model-discussion/18cf69b4/images/branching_model.png)

This branching model assumes:

* that the project uses [semantic versioning](semver.org)
* that the project strictly adheres to a fork-and-pull-request workflow

This branching model can ensure that the proper definition of bugfixes and new
features is enforced.

## Branch semantics

3. `master` gathers work towards the next **minor** _and/or_ **major** release.
1. `release` branches are minted from `master` when a new **major** release
   _or_ when a new **minor** release in a series are ready.
   For example, 1.0.0 and 1.1.0 branch off of `master`.
2. `release/X.Y.Z` branches collect all **patch** releases to a given X.Y
   release series.
3. In each **minor** series, i.e. `release/1.0.Z`, **no new features** are
   added, only bugfixes. Each new bugfix requires a bump in **patch** number,
   signalled by _tagging_
4. Important bugfixes in a given `release/X.Y.Z` can, if necessary, be ported
   to `master` by _cherry picking_
5. Important bugfixes in `master` can, if necessary, be ported to
   `release/X.Y.Z` by _cherry picking_
6. When a new **major** and/or **minor** release is minted, i.e. the
   corresponding branch is created, support for previous versions can be
   dropped. Bugfixes to previous versions are only released if a suitable PR
   addresses them.

## Pull requests (PRs)

1. PRs from any fork should __never__ start from the branch to which they are
   directed in the upstream repository.
  This is why this is a [good idea](http://blog.jasonmeridth.com/posts/do-not-issue-pull-requests-from-your-master-branch/)
2. **Bugfix PRs** are directed towards the relevant `release/X.Y.Z` upstream branch.
3. **Feature PRs** are directed towards the `master` upstream branch.

_Image served thanks to [rawgit.com](https://rawgit.com)_
