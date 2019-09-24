# Build Gatsby Page Slugs Dynamically from Markdown with gatsby-node.js

Now we want to our lists of titles clickable so let's do that by importing `Link` from `gatsby`.

  ```JS
 import React from "react"
 import { graphql, Link } from "gatsby"
 import Header from "../components/Header"

 const Layout = ( {data}) => {
   const { edges } = data.allMarkdownRemark
   return (
     <div>
      <Header />
      {
        edges.map(edge => {
          const { frontmatter } = edge.node
          return (
            <div key={fronmatter.path}>
              <Link to={fronmatter.path}>
              {frontmatter.title}
              </Link>
            </div>
          )
        })
      }
     </div>
   )
 }

 export const query = graphql`
  query HomepageQuery {
    allMarkdownRemark(sort: {order: DESC, fields: [frontmattter___date]}) {
      edges {
        node {
          frontmatter {
            title
            path
            date
          }
        }
      }
    }
  }
 `
 export default Layout
 ```

 Now if you try clicking those links you'll receive a **404 Error** and that's because at the moment these pages don't currently exist.

 In order for Gatsby to create the pages that we need for each of our blog posts, we need to create a file called `gatsby-node.js` inside the root of the directory.

 Inside our `src` directory we're going to create a `templates` folder. Inside that folder we'll create a new file called `blogPosts.js`.

 Inside the the blogPost file type:

 ```JS
import React from "react"
import { graphql }

const Template = props => {
  return (
    <div>
      Blog Post Here
    </div>
  )
}

export default Template
 ```

 There are several APIs that gatsby gives us access to. To create pages we're going to use the createPages API.

 In `gatsby-node.js` inlcude the follwing:

 ```JS
 const path = require('path')
 exports.createPages = (({graphql, actions}) => {
   const { createPages } = actions

   return new Promise((resolve, reject) => {
     const blogPostTemplate = path.resolve('src/templates/blogPost.js')

     resolve(
       graphql`
       query {
         allMarkdownRemark {
           edges {
             node {
               frontmatter {
                 path
               }
             }
           }
         }
       }
       `
     ).then(result => {
       result.data.allMarkdownRemark.edges.forEach(({node}) => {
         const path = node.fronmatter.path
         createPage({
           path,
           component: blogPostTemplate,
           context: {
             pathSlug: path
           }
         })

         resolve()
       })
     })
   })
 })
 ```

 Above we did a little destructuring for `graphql` and `action`. Now we'll destruct `createPage` from actions. Our createPages fuction will return a new promise due to the async nature of file creation. 

 The Promise will take in two arguments, `resolve` and `reject`.

 We need access our blog template so that's where `const blogPostTemplate` comes into play. We'll send it to the path of our directory for our template `src/template.blogPost.js` via `path.resolve`. Be sure that you require path at the top of your file `const path = require('path')`.

 We'll resolve the promise with a call to GraphQL. And then we'll pass in our query as seen above.

 Then we'll add a `then` where we pass the results to a function. `result` contains a data object with the shape with the shape that matches our query. Remember that `edges` are a path to the filesystem node. So with this in mind we're going to do a `forEach`, and for each of our edges we're going to extract the path from our frontmatter.

 We can next call the createPage action. The first parameter is a path for the page URL. And then the component to render `component: blogPostTemplate`. And the third parameter is a `context` object that will make it's way into our blogPost template component as the prop. We want the template to know what the path to our file is `pathSlug: path`. The value of path is what is supplied in our frontmatter.

 After our call to the createPage we'll resolve out of the promise.

 Since we made changes to `gatsby-node.js`, we need to restart our develompent server. So `ctrl + c (⌘ + C for mac users)` and start the server up again with `gatsby develop`.

 Now our blog posts match our blogPost template.