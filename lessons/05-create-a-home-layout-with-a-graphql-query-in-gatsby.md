# Create a Home Layout Component with a GraphQL Query in Gatsby

Inside your `src/pages` directory and open the `index.js` file.

You will notice that we have a simple component that returns `Hello world!`:

```JS
import React from "react"

export default () => <div>Hello world!</div>
```

Now refactor that component to this:

```JS
import React from "react"

const Layout = () => {
  return (
    <div>
      Hello World
    </div>
  )
}

export default Layout
```

Now in order to bring data into our Layout component we have to import `StaticQuery` and `graphql` from `gatsby`:

```JS
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const Layout = () => {
  return (
    <div>
      Hello World
    </div>
  )
}

export default Layout
```

Now let's create a new component called `Header` and let's have it will return our StaticQuery component. And one of the props that the StaticQuery returns is our actual GraphQL query:

```JS
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const Header = () => {
  return (
    <StaticQuery 
      query={graphql`
        query {
          site {
            siteMetadata {
              title
              description
            }
          }
        }
      `}
    />
  )
}
const Layout = () => {
  return (
    <div>
      Hello World
    </div>
  )
}

export default Layout
```

Inside of our query prop we're going to pass a tagged templated with the syntax we use to make a GraphQL query:

```JS
graphql`
  query {
    ...
  }
`
```

And you can use the same syntax that you used in your GraphiQL.

The next prop that we pass to `StaticQuery` is what we want to render.

```JS
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const Header = () => {
  return (
    <StaticQuery 
      query={graphql`
        query {
          site {
            siteMetadata {
              title
              description
            }
          }
        }
      `}
      render={data => <div>{data.site.siteMetadata.title}}
    />
  )
}
const Layout = () => {
  return (
    <div>
      <Header />
    </div>
  )
}

export default Layout
```

Now we're able to replace our `Hello world!` with our `Header` component.

Let's clean up our the our render prop by creating a new component:

```JS
import React from "react"
import { StaticQuery, graphql } from "gatsby"

const TitleAndDescription = ( {data}) => {
  const title = data.site.siteMetadata.title
  const description = data.site.siteMetadata.description

  return (
    <div>
      <h2>{title}</h2>
      <p>{description}</p>
    </div>
  )
}

const Header = () => {
  return (
    <StaticQuery 
      query={graphql`
        query {
          site {
            siteMetadata {
              title
              description
            }
          }
        }
      `}
      render={data => <TitleAndDescription data={data}>}
    />
  )
}
const Layout = () => {
  return (
    <div>
      Hello World
    </div>
  )
}

export default Layout
```

Now you can see that our page has been updated.