---
title: "Deploy"
weight: 8
draft: false
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

- Generate the content with the `hugo --minify` command
- Go to the `public` folder (you are on the other worktree now), commit everything and push it to gh-pages

### Automated

One of the last additions of Github are _actions_, that let you automate a lot of process on your repo. We can use them to update the content of our gh-pages branch each time we push to master.

- Generate a github token with this command: `ssh-keygen -t rsa -b 4096 -C "yourmail@domain.com" -f gh-pages -N ""` remember to change the email. That will create two files: **NEVER COMMIT THEM**. You can move them to a different location to be sure.
- On your github's repo page, go to _settings_
- Click on _deploy keys_ and _add deploy key_
- Choose the name you want, tick the _allow write access_ checkbox and copypaste the content of the `gh-pages.pub` file on the big textarea
- Save
- Click on _secrets_ and _add a new secret_
- Set *GH_PAGES_KEY* as name, and copypaste the content of the `gh-pages` file on the big textarea and save

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
    - uses: actions/checkout@master
      with:
        # Not needed if you are not setting the theme as a submodule
        submodules: true

    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        # Keep the version and extend parameter on track with your local version
        hugo-version: '0.58.3'
        extended: true

    - name: Build
      run: hugo --minify

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v2.4.0
      env:
        # Use the same name that you have set on your githug settings
        ACTIONS_DEPLOY_KEY: ${{ secrets.GH_PAGES_KEY }}
        PUBLISH_BRANCH: gh-pages
        PUBLISH_DIR: ./public
```

- Commit and push the file

PS. To remove the gh-pages branch locally do this:

```shell
rm -rf public
git worktree prune
git branch -D gh-pages
```

## Netifly

- Go to [netlify](https://www.netlify.com/) and register with your github account.
- `Sites` -> `new site from Git`, authorize netlify and select the repository
- Once it's done, close the modal and click on the repo's name (on netifly) to configure it
- Here you can select a different branch to publish from. Leave build command (hugo) and publish directory (public) as they are.
- Click `deploy site`
- Go to `settings` -> `domain management` and select a more suitable domain name for your app.

For a normal Hugo site, you won't need much more (apart for updating the baseUrl on your `config.toml`) but multilanguage sites are a bit special.

- On the `config.toml` remove the `baseUrl` param for both languages and set it as `baseURL = "/"` at the main level
- Create a new `netlify.toml` file and copy paste this code on it:

```toml
[build]
  publish = "public"
  command = "hugo --gc --minify"

[build.environment]
  # Keep this synced with your local version
  HUGO_VERSION = "0.58.3"

[context.production.environment]
  HUGO_ENV = "production"
  # Update with your url
  HUGO_BASEURL = "https://momcorp.netlify.com/"

[context.deploy-preview]
  command = "hugo -b $DEPLOY_PRIME_URL"

[context.deploy-preview.environment]
  HUGO_ENABLEGITINFO = "true"
```

Commit, push, and wait for the deploy to finish. That should made the trick.

There is much more things that can be configured on this platform, like having a "test deploy" for each pull request (with a temporal url), but this is out of the scope.

If you are having problems building the site, go to `settings` -> `build & deploy` and check that the build image is Ubuntu Xenial 16.04.
