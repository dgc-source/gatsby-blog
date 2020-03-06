# Install Plugins for Transforming Markdown with Gatsby

We're going to use `Markdown` files to build our blog.

**Markdown** is a lightweigt markup language that you can use to add formating elemetns to plaintext text docuements.

Check out these two resources to get a better understanding of Markdown:

1. [Markdown Guide](https://www.markdownguide.org/getting-started)
2. [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

In order to use the markdown files in our Gatsby site we're going to need to install two plugins: `gatsby-source-filesystem` and `gatsby-transformer-remark`

`npm install --save gatsby-source-filesystem gatsby-transformer-remark`

`gatsby-source-filesytem` is what is known as a **Source Plugin**. Data in Gatsby sites can come from anywhere: APIs, databases, CMSs, local files etc.

Source plugins fetch data from their source. E.g. the `filesystem` source plugin knows how to fetch data from the file system. This source plugin lets you query data about a file.

`gatsby-transformer-remark` is what is known as a **Transformer Plugin**. Tranformer plugins take raw content from source plugins and transforms it into something more usable. Take markdown files for example. Markdown is nice to write in but when you build a page with it, you need the markdown to be HTML. That's where this plugin really shines.

So what you want to do next is create a configuration file for your plugins. So in your main directory of your site, create a file called `gatsby-conifg.js`.

Inside this file you can create the metadata for this site:

```JS
module.exports = {
  siteMetadata: {
    title: `My Blog`,
    description: `This is my cool blog`,
  },
}
```

Now to the same configuration file we want to add in our plugins that we installed:

```JS
module.exports = {
  siteMetadata: {
    title: `My Blog`,
    description: `This is my cool blog`,
  },
  plugins: [
    `gatsby-transformer-remark`, {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `pages`,
        path: `${__dirname}/src/pages`,
      },
    },
  ],
}
```

Notice how for the `gatsby-source-filestyem` we passed in an object instead of just it's name. That is because this plugin has the ability to pass in options.

Since we made changes to `gatsby-config.js`, we need to restart our develompent server. So `ctrl + c (⌘ + C for mac users)` and start the server up again with `gatsby develop`.
