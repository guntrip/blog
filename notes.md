## Stevecat's Jekyll Blog

I've had a lot of fun with this and in the process, made it rather complicated. Eek.

### Articles

Any post with the `articles` category will be featured on this page.

### Galleries

I've written a simple gallery in the `photos.html` include (`_includes/photos.html`). An example of a simple gallery is below:

```
---
layout: default
photosFolder: phobophobia
photosShowTitle: true
photos:
  - file: fear_tinfoil.jpg
    title: "\"Tin Foil. The cheap thin kind.\" - Metallophobia"
  - file: fear_sharks.jpg
    title: "\"Sharks.\" - Selachophobia"
  - file: fear_heights.jpg
    title: "\"Heights.\" - Acrophobia"
---
<h1>Phobophobia</h1>
{% include photos.html %}
```

It's simple right now but if I ever decide to incorporate something fancy, I won't have much to change.

### Projects

Projects are special posts that have the following YAML front matter in additional to regular posts:

`snippet`: text to display on the projects page.
`image`: a link to an image, in `assets/images/projects` to use with the project.
`project_type`:

* `self`: blog post, will just be included as is with linked posts.
* `photography`: will link to the photo gallery set in `project_gallery`.
* `url`: will link to an external URL (set as `project_url`).

`linked_posts`:

* Array of individual posts that are related to this project (full filename, i.e. `2017/2017-02-05-frame-wood.markdown`). These then build the table of contents and are all output on the project page.

**Note:** Jekyll does not _always_ render the markdown and liquid tags in these posts. Sometimes it will, sometimes it won't. For this reason, any post shown on this page is run through the `markdownify` filter. This will catch markdown but not liquid tags. Booo.
