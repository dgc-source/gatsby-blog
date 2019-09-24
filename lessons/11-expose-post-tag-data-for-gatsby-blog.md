# Expose Post Tag Data for a Gatsby Blog

Create two new files `allTagsIndex.js` and `singleTagsIndex.js`

In `allTagsIndex.js` add the following lines:

```JS
import React form "react"
import { graphql, links } from 'gatsby'

const AllTagsTemplates = ({data}) => {
  return (
    <div>
     <div>
       tags here
    </div>
  )
}

export defualt AllTagsTemplate
```

Our `singleTagIndex.js` page will be pretty much the same. Now, let's open up

Go to `gatsby-node.js` and create a new function called `createTagPages`.

`createTagPages` will take in createPage and the list of posts. .

```JS
  const createTagPages = (createPage, posts) => {
  const allTagIndexTemplate = path.resolve('src/templates/allTagsIndex.js')
  const singleTagIndexTemplate = path.resolve('src/templates/singleTagIndex.js')
}
```

```JS
const postByTag = {}

posts.forEach(({node}) => {
    if (node.frontmatter.tags) {
      node.frontmatter.tags.forEach(tag => {
        if(!postsByTag[tag]) {
          postsByTag[tag] = []
        }
        postsByTag[tag].push(node)
      })
    }
})
```

we are ynamically creating a key for each of our tags. Each of those keys will have an array of the posts that use that tag. We should have a built up object that has each of our tags represented with an array of nodes for each one. Now, we'll create a master list of all of the tags. We'll do const tags = Object.keys(postsByTag).

Now call createPage. Our path will be `'/tags'`. The component will be the `allTagsIndexTemplate`. The context that we're going to pass will be called tags and it will be tags.sort, so this will be a sorted list of all of our tags.

```JS
const tags = Object.keys(postsByTag)

createPage({
path: '/tags'
component: allTagsIndexTemplate,
context: {
tags: tags.sort()
}
})
```

Before we process each of our posts, we're going to call our createTagPages function with our createPage action and all the posts that we created.

```JS
const posts = result.data.allMarkdownRemark.edges

createTagPages(createPage, posts)
```

Restart gatsby develop. Now on our /tags page, I can hit reload, and we see 'tags here' from our template, which is good. That means that our /tags page is being created.

```JS
const AllTagsTemplate = ({data,pageContext}) => {

console.log(pageContext)
return (

<div>
  <div>
    tags here
  </div>
</div>)
}
```

Data is what's used for a query that would be inside of this template and pageContext is what gets passed from gatsby-node.js.

In your query be sure to include the tags key:

```JS
  edges {
    node {
      frontmatter {
      path
      title
      tags
      }
    }
  }
```

Remember, whenever you make changes to `gatsby-node.js` restart your server.

Markdown File Example for Tags

In gatsby-node.js this is our main createPages export. What we're doing here is we're looking for all of the markdown files inside of the `src/pages` directory.

We're calling our createTagPages function which is creating this index of all tags.
