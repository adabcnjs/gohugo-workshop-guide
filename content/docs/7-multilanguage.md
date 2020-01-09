---
title: "Multilanguage"
weight: 7
draft: false
summary: "Having our content available on different languages is very important in a multinational world. With Hugo and the correct theme new languages can be configured in no time, and maintenance is almost none."
---

As many other features, multilanguage :globe_with_meridians: support varies depending on the theme you have choosen, so take that into consideration when selecting one for your site.

## Configuring languages

We can declare as many different languages as we want in the `config` file. The minimun parameters to specify are declare the variable itself and the weight (which will be taken into account for language fallbacks. More on that later)

```toml
[languages]
  [languages.en]
    weight = 1
  [languages.es]
    weight = 2
```

We will add more things here later.

## Translating the content

We can see our spanish language on the top bar, but if we click there the site looks empty. Content still needs to be translated.

There are two ways to do it: **per file** or **per folder**. Both methods are good, choosing one or the other just depends on what fits you better.

:page_facing_up: Per file, you just need to edit your markdown file names adding the language code using the same key as in the site config. For example, instead of `bender.md` we will have `bender.en.md` and `bender.es.md`.

:open_file_folder: Per folder, add one folder for each language just under your `content` directory, and nest your articles in there. This way you will have `content/robots/en-EN/bender.md` and `content/robots/es-ES/bender.md`. As you can see, the folder name doesn't need to be the same as the language key. Instead, you need to add it to the configuration:

```toml
[languages]
  [languages.en]
    weight = 1
    contentDir = "content/en-EN"
    languageCode = "en-EN"
  [languages.es]
    weight = 2
    contentDir = "content/es-ES"
    languageCode = "es-ES"
```

**Important** `languageCode` is used to set up the `lang` attribute on our html tag, so it can affect screen readers, rss feeds, etc. Don't forget to set it correctly!

## Dynamic configuration

Translating the content is the main work, and some parts are magically translated too, but that is not enough.

We may want to change general settings like the site title, urls, etc: this is easily done duplicating the configuration keys under every language. Some of them can be defined directly, some need to be written with dots. Check [the docs](https://gohugo.io/content-management/multilingual/#readout) for the correct sintax.

`baseUrl` is tricky, because you need to redefine it for every language, you cannot just do it for one and expect the rest to fallback on the default language. The good part is that Hugo will built two different sites, so you could have totally different domains (and the link between them will stil work!)

In my case, I added did this customizations for spanish:

```toml
[languages.es]
  weight = 2
  contentDir = "content/es-ES"
  title = "Corporación Mamá"
  baseURL = "http://example.es"
  [languages.es.taxonomies]
    habilidad = "habilidades"
  [[languages.es.menu.main]]
      url = "https://futurama.fandom.com/es/wiki/Mam%C3%A1"
      name = "Wiki"
      identifier = "wiki"
```

Some interesting things to point out:

- _tags_ is not redefined, since I prefer the word in english so it will just use the fallback
- You could add extra sections on the menu just for a specific language.
- Not only texts are configurable, we can change any other configuration parameter.
- The _Ananake_ theme does not support it, but other themes may let you set a `languageName` key or similar on the configuration to show that instead of the language code.

## Translating content inside templates

If you have navigated to a _divisions_ post, you'll have noticed that, of course, the _division-info_ shortcode is not translated.

On the other hand, some theme texts are already translated. Navigate to the home in spanish and take a deeper look. How does this magic work and how can we use it?

The trick is in the theme's `i18n` folder and Hugo (Go) translating function.

We need to create a `i18n` folder in the root of the project, and add language files following the pattern that you can see on the theme folder. Luckily for us, Hugo is smart and in this case won't overwrite the theme translated keys, but add up all of them.

Add the new translations needed and the modify the shortcode to use them!

## What about dates?

You may be thinking "ey, my blog post date is not being translated!" and you are right. There is still not a good solution to do it since Go does not support it, but the official docs propose a [workaround](https://gohugo.io/content-management/multilingual/#translation-of-strings).

Another option is to use a numeric format and different templates per language (`single.es.html` for example), to show the numbers in the correct order.

None of this options is good enough, and both involve unnecesary manual work. However, the Hugo team is always trying to improve their product and this may change in the future.

---

There are more things that may be of interest, like how to have different resources for each language (images, attached files, etc), customizing the urls for the articles, etc. They are covered in this [very nice article](https://regisphilibert.com/blog/2018/08/hugo-multilingual-part-1-managing-content-translation/)
