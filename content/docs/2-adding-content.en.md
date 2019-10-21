---
title: "Adding Content"
date: 2019-10-17T23:37:54+02:00
weight: 2
draft: false
---

## Creating content

There are two ways of adding content to a Hugo site: with Hugo's command line tool or manually.

To add content from the command line run `hugo new robots/killbot.md`. A new file will appear. Try writing on it using markdown syntax and see what happens on your site! (keep running `hugo serve` in a different terminal for a faster development)

You can also create the files manually.

Although markdown is the most common, Hugo accepts also:

- Mmark
- Org
- Html
- [Emojis! :dancer:](https://gohugo.io/content-management/formats/#emojis). Yeah, not a filetype. Deal with it :sunglasses:

## Order matters

The way you organize your content in folders is very important with Hugo. It will be used to choose the default layout, menu, urls and the related media. All this values can be changed if needed on the _Front Matter_ (the top section between dashes).

Let's add some content to our killbot page. Create a `static/images` folder at the same level as `content` and put an image of a killbot in there. You can insert that on `killbot.md` with `![](/images/theimagename.png)`.

Apart from that, each folder inside content can have one `_index.md` page, called the _list_ page, and it will be used as a "home" for that category. Let's do an index for our robots section! :robot:

PS: There's also the option of organizing the content with [page bundles](https://gohugo.io/content-management/page-bundles/) which I find tidier :broom: but a bit more confusing at the beginning.

## Generic pages

As you can see, some pages are automatically generated (like the home page, the 404, or the list sections). Those are provided by the theme, but can be overriden easily.

We are going to adapt the error page a little bit. First, look for the actual one on `themes/ananke/layouts/404.html`, and copy all of it on `layouts/404.html`. Then modify whatever you want.

This works to modify almost every file you can find on a theme: copy it following the same path on your project's root and Hugo will use it instead.
