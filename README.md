# monorepo-deploy

[![CircleCI](https://circleci.com/gh/ButterflyNetwork/monorepo-deploy/tree/develop.svg?style=svg)](https://circleci.com/gh/ButterflyNetwork/monorepo-deploy/tree/develop)

A sample deployment monorepo with git submodules, using CircleCI.

Submodule changes are detected using the [git-submodule-changes](https://github.com/ButterflyNetwork/git-submodule-changes-orb) orb.

## Usage

Clone the repo:

```bash
~/src$ git clone git@github.com:ButterflyNetwork/monorepo-deploy.git
~/src$ cd monorepo-deploy
```

This repo keeps track of the deployed revisions as Git submodules. Update submodules to match remote in your local checkout before making any changes, by running, in the repo root:

```bash
~/src/monorepo-deploy$ git submodule update --init
```

To update a specific repo, go into the submodule and check out the desired commit:

```bash
~/src/monorepo-deploy$ git checkout -b update
~/src/monorepo-deploy$ cd project-one
~/src/monorepo-deploy/project-one$ git checkout develop
~/src/monorepo-deploy/project-one$ git pull
```

Go back to the repo root and commit this as an update to the repo:

```bash
~/src/monorepo-deploy/project-one$ cd ..
~/src/monorepo-deploy$ git add project-one
~/src/monorepo-deploy$ git commit
```

Submit this as a PR. When you merge the PR, CircleCI will run a workflow that "deploys" only the repos/submodules that were changed.
