---
title: "Set up"
date: 2019-10-17T23:04:37+02:00
weight: 1
---

## Create a project

To install Hugo, follow the [instructions](https://gohugo.io/getting-started/installing) on the site, depending on your operating system. You may need to restart the console afterwards for it to be activated.

Once it is installed, **create a new site** with `hugo new site momcorp`. Then move to the new folder with `cd momcorp` and start a git repository in there (`git init`), or set the origin to an already existing one.

Setting up git is optional, but will be helpfull on the next step.

## Add a theme

To start showing content, Hugo needs a theme. You can create those on your own, but Hugo has a huge and amazing community that has already built and shared a lot of themes. You have some interesting ones [here](https://themes.gohugo.io/), but for the purpose of this workshop we will use [this one](https://github.com/budparr/gohugo-theme-ananke).

The usual way to install Hugo themes is adding them as a git submodule: `git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke`.

Last, configure Hugo to use that theme adding `theme = "gohugo-theme-ananke"` on the `config.toml` file that it's on the root of the project.

This is the file were you are going to set up all the configuration for Hugo, including the theme and language options. But we will deal with that later!

## Run the project

There is no content yet, but we can run the project to see the main scheme of our theme. Just run `hugo serve` (in the same folder where config.toml is) and open [http://localhost:1313](http://localhost:1313) on your browser.
