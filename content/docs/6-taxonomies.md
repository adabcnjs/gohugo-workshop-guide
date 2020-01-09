---
title: "Organizing content: taxonomies"
weight: 6
draft: false
summary: "Tags are more common on blogs, to categorize the posts and allow the users to discover new content, but they can be also usefull for normal sites"
---

When we have a lot of content, we usually want to categorize it so our users can easily find what they are looking for. For this purpose, Hugo can group content by **taxonomies**.

By default, there are already two taxonomies: _tags_ and _categories_, but it is also easy to create custom ones.

## Using taxonomies

Taxonomies are added on the _Front Matter_ of each page, as arrays of strings. For example, lets give our Santa robot a "unique model" tag setting it's _Front Matter_ as:

```yaml
---
title: "Robot Santa Claus"
tags: ["unique model"]
---
```

If you refresh and go to the Santa page, you'll see the tag at the bottom. The way taxonomies are shown depends on the chosen theme. For example, in this one categories are not shown.

Additionally, Hugo generates list pages for all your taxonomies, so you can click on the _unique model_ link and see a list of all the robots with that same tag. You may need to restart your server (`ctrl + C` and `hugo serve` again) to see it correctly.

## Creating custom taxonomies

We can define any other taxonomy for our pages. For example, we could add an _habilities_ taxonomy so we can list the robots by function.

When creating a custom taxonomy, we need to set it on the `config.toml` file, so Hugo can generate all the listing pages and so. It uses a `singular = "plural"` structure, like this:

```toml
[taxonomies]
  hability = "habilities"
  tag = "tags"
```

As you can see, you need to redefine the default taxonomies that you want to keep (we are dropping _categories_ in this case).

Of course, for this custom taxonomies to appear on the site, the theme has to support that (or you can modify a layout to show them!). In any case, the list page is always available under `yoursite/taxonomy-name/taxonomy-value`. Check the official docs to see some examples of [layouts related to taxonomies](https://gohugo.io/templates/taxonomy-templates/).

## Disabling taxonomies

If you aren't going to use taxonomies and want to prevent the list pages to be created, just add `disableKinds = ["taxonomy", "taxonomyTerm"]` to the configuration.
