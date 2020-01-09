---
title: "Shortcodes"
weight: 4
draft: false
summary: "Shortcodes add superpowers to markdown, allowing to insert dynamic HTML code. There are some already built-in, but we can easily create our own or copy the shortcodes shared by the community"
---

Using markdown for our content has advantages, but it is kinda boring. There's no way to insert fancy content like videos, images carousels, tweets... shortcodes to the rescue!

## Using shortcodes

Shortcodes are a way to introduce dynamic, reusable pieces in our source content. Hugo comes with some [built-in shortcodes](https://gohugo.io/content-management/shortcodes/).

There are two ways to use a shortcode, usually depending if they process markdown or not:

- With markdown: `{{%/* shortcodename */%}}Stuff to _process_ in the *center*.{{%/* /shortcodename */%}}`
- Without markdown: `{{</* shortcodename */>}} A bunch of code here {{</* /shortcodename */>}}`

They can also take parameters, named or not.

For example, to add a video on the _divisions_ main page we can use:

```
{{</* youtube _rt7wSMIs7I */>}}
```

## Custom shortcodes

Custo shortcodes are easy to do, and can get as powerfull (and complex) as you want.

On it most basic form, custom shortcodes are just html files that lie on the `layouts/shortcodes` folder. Hugo automatically detects them and you can insert them using the file name as shortcode name.

Lets say we want a better way to add our divisions information.

- Create a `shortcodes` table in the already existing `layouts` folder.
- Add a `division-info.html` file with some html structure to show the information. For example:

```html
  <dl>
  <dt>Official name:</dt>
  <dd></dd>
  <dt>Creation date:</dt>
  <dd></dd>
  <dt>CEO:</dt>
  <dd>Mom</dd>
  <dt>COO:</dt>
  <dd></dd>
</dl>
```

- The data can be added as shortcode parameters or inner content. Check the [docs](https://gohugo.io/templates/shortcode-templates/#access-parameters) to see the different ways to do it.

- Insert the shortcode on each division passing the data as correspond.

You have a lot of examples of shortcodes [here](https://github.com/gohugoio/hugo/tree/master/docs/layouts/shortcodes) and [here](https://github.com/spf13/spf13.com/tree/master/layouts/shortcodes).

In shortcodes you can use all the [Hugo functions](https://gohugo.io/functions/).
