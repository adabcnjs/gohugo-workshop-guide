---
title: "Configuring themes and menus"
date: 2019-10-21T22:26:54+02:00
weight: 3
draft: false
summary: Themes have different options to be configured, and getting to know the one that you are using leads to a better experience. This will allow you to customize the theme and manipulate the items shown in the different menus.
---

Most of Hugo's themes have little to no documentation, but they usually have a demo site that is a good showcase to check what can be done. Some of them won't even work with a special configuration, so it is an easy start to just copy-paste the `config.toml` on the example site to our own.

Using our theme [documentation](https://github.com/budparr/gohugo-theme-ananke) try to set a background image for the home (where the Paris landscape is on the demo) and the "subtitle".

## Adding entries to menus

One common thing about themes, is that they show you menus on some places. Some of them may add your content to the menus automatically (or maybe just if you nest it on a specific folder) but usually you need to define what goes there.

To add an entry (usually a _list type_) to the main menu, add `menu: "main"` to the _Front Matter_. Different themes can define diferent names for their menus, but _main_ is a common one. Do it with our `robots/_index.md` to have a quick access to the list of robots.

It's also possible to add entries on the `config.toml` file. The main advantage is that this allows to define menus without creating a new content page. **Both systems are compatible**.

For example, let's add an external link to our menu. The syntax is as follows:

```
[menu]

  [[menu.main]]
    identifier = "wiki"
    name = "Wiki"
    url = "https://futurama.fandom.com/wiki/MomCorp"
```