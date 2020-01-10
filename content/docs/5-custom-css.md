---
title: "Custom CSS"
weight: 5
draft: false
summary: "Different themes allow for different levels of personalization, but adding our personal touch is something that everybody wants. Don't be shy and dig into your theme to customize it!"
---

Customizing our theme is something that we all need. From the simple "change the main color" to more complex styles, this is a normal need.

Unfortunately for us, there is no built-in way to do this with Hugo :sweat:. It depends on the theme you are using, so my advice is to take this point in consideration when choosing one.

Some situations you can find are:

- You can add your own CSS/SCSS files. From example, with [call me sam](https://github.com/victoriadrake/hugo-theme-sam#editing-the-theme)
- You can select a "theme" from a list, or set some variables (main color, font, etc). For example, the [learn theme](https://learn.netlify.com/en/basics/style-customization/#theme-variant)
- You need to edit the source CSS/SCSS files to customize it.

Depending on how it is done, some times you'll be able to "duplicate" the files on your main project folder (the same way you "duplicate" the templates) to override them, but other times you can't.

In this case it may be easier to apply the styles inline in the shortcodes, templates, etc.

Another workaround is duplicating the correct layout and adding a `<link rel="stylesheet">` pointing to our custom css file.

----

Checking our theme's documentation, we'll discover that we can add our custom css files setting the config this way:

```toml
[params]
  custom_css = ["css/styles.css"]
```

And then adding our styles at `static/css/styles.css`. We could use more than one css file if needed, since the `custom_css` parameter is an array.
