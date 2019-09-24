# Add Next and Previous Links to a Gatsby Blog

To make the navigation a lot smoother for users we're going to add next and back to our blog.

Add a variable to the `gatsby-node.js` file as well as update the reamining code for our `forEach`:

```JS
const post = results.data.allMarkdownRemark.edges
posts.forEach(({node}, index) => {
  const path = node.frontmatter.path
  createPage({
    path,
    component: blogPostTemplate,
    context: {
      pathSlug: path,
      prev: index === 0 ? null : posts[index - 1].node,
      next: index === (posts.length - 1) ? null : posts[index + 1]
    }
  })
})
```

`prev: index === 0 ? null : posts[index - 1].node,` - this is for the post that comes before it. This says that if the index is equal to zero then there is no other previous post, but if it's not equal to 0 then there is another post.

`next: index === (posts.length - 1) ? null : posts[index + 1]` - this is for the post that comes after it. This is says that if index is equal to the last post then are no other posts left and if not then this is another post remaining.

When we add keys to the `createPage` call it ends up in our blogPost template under a key called `pageContext`. To verify this do a console log of your props object.

inside this `pageContext` you're see the keys for `path`, `next` and `prev`.

When you first look at the result of the query you'll know that it's out of order. The first post should not contain a previous post. So in `gatsby-node.js` add a sort to `allMarkdownRemark`

```JS
graphql(`
  query {
    allMarkdownRemark(sort: {order: ASC, fields: [frontmatter___date]})
  }
  ....
`)
```

Restart your server.

Next go to your blogPost.js and add the following lines which let you navigate to your next and previous posts.

```JS
import React from "react"
import { graphql, Link } from "gatsby"

const blogPost = ({ data, pageContext }) => {
  const {next, prev} = pageContext
  const { markdownRemark } = data
  const title = markdownRemark.frontmatter.title
  const html = markdownRemark.html
  return (
    <div>
      <h1>{title}</h1>
      <div className="blog-post" dangerouslySetInnerHTML={{ __html: html }} />
      {
        next &&
        <Link to={next.frontmatter.path}>
          Next
        </Link>
      }
      {
        prev &&
        <Link to={next.frontmatter.path}>
          Next
        </Link>
      }
    </div>
  )
}

export const query = graphql`
  query($pathSlug: String!) {
    markdownRemark(frontmatter: { path: { eq: $pathSlug } }) {
      html
      frontmatter {
        title
      }
    }
  }
`

export default blogPost
```
