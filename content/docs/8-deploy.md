---
title: "Deploy"
weight: 8
draft: true
---

We are almost finished! :tada: You have a multilanguge site, fast and responsive, and adding new content is a piece of cake. Amazing. Let's get it public!

Deploying your site to the internet is not part of what Hugo pretends to do, but for the purpose of this workshop I'll go over two different options on how you can do it.

## Github pages

### Set up

Gihub provides a free domain and hosting for each repo, even on free accounts. It has some limitations, but it's perfect for static websites (like ours) that are not going to get a lot of traffic. This is how to activate it:

- Execute the following comands to create an orphan branch called `gh-pages`

```shell
git checkout --orphan gh-pages
git reset --hard
git commit --allow-empty -m "Initializing gh-pages branch"
git push origin gh-pages
git checkout master
```

- Open your repo's github, and login.
- Click on _settings_
- Scroll almost to the bottom of _options_ until you see the _Github Pages_ card
- On the _source_ dropdown, choose _gh-pages branch_.

Now, everything you push to that branch is going to be the content of your website

- Get the url that github provides and add it as your `baseURL` in the `config.toml` file
- Get your branch locally and link it to the `public` folder using the _worktree_ git's feature:

```shell
rm -rf public
git worktree add -B gh-pages public origin/gh-pages
```

### Manual deploy

- Generate the content with the `hugo` command
- Go to the `public` folder (you are on the other worktree now), commit everything and push it to gh-pages

### Automated

One of the last additions of Github are _actions_, that let you automate a lot of process on your repo. We can use them to update the content of our gh-pages branch each time we push to master.

- Generate a github token with this command: `ssh-keygen -t rsa -b 4096 -C "pcalabriarubio@gmail.com" -f gh-pages -N ""` remember to change the email. That will create two files: **NEVER COMMIT THEM**. You can move them to a different location to be sure.
- On your github's repo page, go to _settings_
- Click on _deploy keys_ and _add deploy key_
- Choose the name you want, tick the _allow write access_ checkbox and copypaste the content of the `gh-pages.pub` file on the big textarea
- Save
- Click on _secrets_ and _add a new secret_
- Set _GH-PAGES-KEY_ as name, and copypaste the content of the `gh-pages` file on the big textarea and save

Now the automated actions can **push** to your repository

- Add a new file to your repo on `.github/workflows/main.yml`. You probably need to create the folders
- Content of the file:

```yml
name: Publish Site

on:
  push:
    branches:
      - master

jobs:
  build-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repo
        uses: actions/checkout@master
        with:
          submodules: true
      - name: Publish Site
        uses: chabad360/hugo-gh-pages@master
        with:
          hugoVersion: extended_0.58.3 # Ideally, keep this synced with your local version
          githubToken: ${{ secrets.GH_PAGES_KEY }}
```

- Commit and push the file

PS. To remove the gh-pages branch locally do this:

```shell
rm -rf public
git worktree prune
git branch -D gh-pages
```

## Netifly
