# Build a Blog Post Template with GraphQL and Gatsby

So inside of our `gatsby-node.js` file we make a query that finds our files and gets the path from the front matter. Then we cycle through all of them and call `CreatePage` which creates a page of each of them using the value of `blogPostTemplate` component. It passes the `context` and `pathSlug` to the props object of our template component.

In our `blogPost.js` console log props and you'll see that there is a `pageContext` key with the value of the path for our post.

In order to get the HTML for our post we have to write a GraphQL query that will search `markdownRemark` for the file that has the path of our blog post.

Over in our `blogPost.js` template write the following:

```JS
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
```

When we write a query, we can then get our `pathSlug` variable by doing `$pathSlug`. This is a `String!`. The exclamation point means that it's required.

In our query we included `markdownRemark` because we're only looking for that individual file.

We're looking for `frontmatter` where the path is `eq (equal)` to the value stored in `$pathSlug`. We want the `html` and the `fronmatter`. From the frontmatter, we want to get the title out.

Remember, `data` gets passed in as a prop to the component from the query. To verify, console log the `props` object.

Now can we fix up our component and display that data that we received from our query:

```
import React from "react"
import { graphql } from "gatsby"

const blogPost = ({ data }) => {
  const { markdownRemark } = data
  const title = markdownRemark.frontmatter.title
  const html = markdownRemark.html
  return (
    <div>
      <h1>{title}</h1>
      <div className="blog-post" dangerouslySetInnerHTML={{ __html: html }} />
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
