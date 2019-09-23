# Format Markdown Files for Gatsby.js

Go to your `src/pages` directory and add in a few directories with the slug `YYYY-MM-DD-name-of-post`.

An example would be: `2018-07-21-first-post`

Inside each of the foders create an `index.md` file.

Inside the `index.md` file add the front matter for the site. **Fronmatter** is information pertaining to each blog post that you can reuse throughout your post.

```YML
---
path: "/first-post"
date: "2019-09-23"
title: "My First Post"
tags: ['this', 'that']
excerpt: "A preview of my first post"
---
```
Make sure that you put the front matter inbetween two sets of three dashes `---`.
Then you can start creating your blog post.

Follow this pattern for all of your posts