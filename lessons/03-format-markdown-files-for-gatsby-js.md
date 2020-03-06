# Format Markdown Files for Gatsby.js

Add in a directory with the slug `YYYY-MM-DD-name-of-post` inside `./src/pages` folder. 

Inside each of the foders create an `index.md` file.

With VSCode, I cheat by staying the root folder & entering: `src/pages/2020-03-06-building-gatsby-blog/index.md`


Inside the `index.md` file add the front matter for the site. **Frontmatter** is information pertaining to each blog post that you can reuse throughout your post.  [Hugo has good Frontmatter](https://gohugo.io/content-management/front-matter/) writeup, but use YAML format & not all fields are supported 'out of the box'.

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
