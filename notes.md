## Stevecat's Jekyll Blog

I've had a lot of fun with this and in the process, made it rather complicated. Eek.

### Topics

Each topic has it's own directory in the `/topics` containing an `index.html` with the following:

```
---
layout: topics
topic: silly
---
```

The topics layout (`_layouts/topics.html`) will show only posts matching the `topic`.

**Note:** the topic counts include projects but these _are_ shown on those views.

**Note:** it's not possible to paginate these pages in Jekyll. I can see how it would be possible manually but I'd rather just have long pages for now :fearful:

### Truncating posts

All posts will be truncated after the number of words set in `break_at` in `_config.yml` - unless `<!--break-->` is present in the post,
then it will break there.

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

Projects are a special type of post and are handled differently and allow you to group posts. If a post has the `projects` topic, and doesn't have `show_on_blog` set to true, it won't be included in the blog. It will however appear on the /projects page. Projects posts have the following YAML front matter in additional to regular posts:

`snippet`: text to display on the projects page.

`project_type`:

* `self`: blog post
* `photography`: will link to the photo gallery set in `project_gallery`
* `url`: will link to an external URL (set as `project_url`)

`linked_posts`:

* Array of individual posts that are related to this project (full filename). Displayed in "Related posts".

Projects are listed on /projects and make use of the `project.html` include. If accessed directly, `full_post` is `true`, the content of the project post will be outputted. If there any linked posts, they will be iterated through and also outputted - with full headers - using `post.html`. The "Related posts" switches to linking to anchor tags inserted in each post for a table of contents.

**Note:** Jekyll does not _always_ render the markdown and liquid tags in these posts. Sometimes it will, sometimes it won't. For this reason, any post shown on this page is run through the `markdownify` filter. This will catch markdown but not liquid tags. Booo.
