# Install the Latest Version of Gatsby

In order to use Gatsby you want to make sure that `Node.js` is installed. The docs state that the best way to install Node is through a package manager known as **Homebrew**. 

copy this command below and paste it into your terminal:

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Check out the official [Homebrew](https://brew.sh/) site to get a deeper understanding of what it is that **Homebrew** does.

Once Homebrew is installed be sure to verify the installation by typing the following into your terminal:

`brew -v`

`Node.js` is an environment that can run JavaScript code outside of a web browser. Gatsby is built with Node.js. To get up and running with Gatsby, you'll need to have a recent version installed on your computer.

To install:
  1. Open your terminal
  2. Run `brew update` to make sure you have the latest version of brew.
  3. Run this command to install Node and npm in one go: `brew install node`
  4. Run node --version to check to see if Node was installed.

Be sure to install `Git`. When you install a Gatsby "starter" stie, Gatsby uses Git behind the scenes to download and install the required files for your starter. So it's important to make sure that you have Git installed.

  1. [Git for macOS](https://www.atlassian.com/git/tutorials/install-git#mac-os-x)
  2. [Git for Windows](https://www.atlassian.com/git/tutorials/install-git#windows)
  3. [Git for Linux](https://www.atlassian.com/git/tutorials/install-git#linux)

The `Gatsby CLI` tool lets you quickly create new Gatsby-powered sites and run commands for developing Gatsby sites. It is a publshed npm package.

The Gatsby CLI is available via npm and should be installed globally by running: 

`npm install -g gatsby-cli`

Make sure to type `gatsby -v` to make sure that you're running greater than version 2.

Next go ahead and type the following into your terminal:

`gatsby new my-blog https://github.com/gatsbyjs/gatsby-starter-hello-world`

This is the minimum that you'll need to start on a Gatsby site.

Go inside the `my-blog` directory and run `yarn` to install all of the dependecies.

If you don't have yarn installed. The official [Yarn](https://yarnpkg.com/lang/en/docs/install/) site has an easy and comprehinsable way of walking you through the installation steps. And what's even cooler is that site checks your current operating system and gives you the steps you need for your setup.

Now run `gatsby develop` and go to local `localhost:8000` to see your newly created Gatsby site. It's not much, but it's definitely a starting point.

