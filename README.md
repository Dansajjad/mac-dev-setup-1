# Mac OSX Development Setup
Lots were copied from [nicolashery](https://github.com/nicolashery/mac-dev-setup)

## System Update
First thing is to update the operating system. On OSX El Capitan: **Apple Icon > App Store... > Updates > Update All**

## System Preferences
After updating your system, you may like to change the name of your computer under the **Sharing** preferences. This will change what name is displayed within the terminal.

## Xcode
We're going to need Xcode for developing iOS apps, so lets download it at this time, as it's a large file:
https://developer.apple.com/xcode/download/

## Google Chrome
Let's get a reliable browser, Google Chrome happens to be my favorite: https://www.google.com/chrome/browser/desktop/

## Consolas
Consolas is a Microsoft font, if you have Microsoft Office installed, it should  already be installed. It's a nice monospaced font for terminal, we'll use a different font and styling for our editor (controlled by a **Theme**).

## iTerm2
The standard terminal is nothing special, let's add some features by getting iTerm2: https://www.iterm2.com/

Drag the unzipped iTerm2 application into the **Applications** folder.

Let's change the styling of our terminal to make it easier to use and much more fun.

First, open preferences in **iTerm**, then under the tab **Profiles**, section **Text**, change the font to consolas 13pt.

Next, we're going to change the color scheme of the console, if you haven't already, open **iTerm > Preferences > Profiles > Colors**, from the **Color Presets** dropdown, select **Solarized-Dark**. It provides some nice colors for iTerm.

Let's tweak the formatting of the console text by downloading the following files from Nicholas Hery's setup guide:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_profile
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.bash_prompt
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.aliases


## Homebrew
Homebrew is a package manager for OSX, its good at installing a select few very important frameworks.

### Install
To install, run this in the command line:

    $ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Might have changed: We need to add the brew install location to the system **PATH** using the **.bashrc** file:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

After install, let's make sure everything is working. After opening a new terminal window, run:

    $ brew doctor

### Usage
To install a **Formula**, run:

    $ brew install <formula>

To update Homebrew's list of forumlae, run:

    $ brew update

To see if any of your packages need to be updated:

    $ brew outdated

To update a package:

    $ brew upgrade <formula>

Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

## Git
Git is the most widely used source control management tool. If you aren't familiar with it, take a look here: http://git-scm.com/

Let's begin by installing **git** through **Homebrew**:

    $ brew install git

After that is finished installing, lets make sure it's working. In a new terminal tab, run:

    $ git -v

This should display the version of git you are running. If it doesn't something went wrong, reinstall and try again.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [InnerSource](https://innersource.accenture.com/) and [SourceTree](https://www.sourcetreeapp.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your remote repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain

**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/nicolashery/mac-dev-setup/blob/master/.gitignore) file for inspiration.

## Atom
Everyone has different preferences about Editors, after using Sublime Text 3 for a while, I tried Atom again and surprisingly really liked it. It has a great built in package manager,

More information can be found here: https://atom.io/

### Atom Packages
I like to install the following Atom packages:
* [jshint](https://atom.io/packages/jshint)
* [autoclose-html](https://atom.io/packages/autoclose-html)
* [file-icons](https://atom.io/packages/file-icons)
* [npm-install](https://atom.io/packages/npm-install)
* [project-manager](https://atom.io/packages/project-manager)
* [todo-show](https://atom.io/packages/todo-show)

and the following themes:
* [atom-material-ui](https://atom.io/themes/atom-material-ui)
* [atom-material-syntax](https://atom.io/themes/atom-material-syntax)
* [atom-material-syntax-light](https://atom.io/themes/atom-material-syntax-light)
* [atom-material-syntax-dark](https://atom.io/themes/atom-material-sytnax-dark)

## Node.js

Install [Node.js](http://nodejs.org/) with Homebrew:

    $ brew update
    $ brew install node

The formula also installs the [npm](https://npmjs.org/) package manager. However, as suggested by the Homebrew output, we need to add `/usr/local/share/npm/bin` to our path so that npm-installed modules with executables will have them picked up.

To do so, add this line to your `~/.path` file, before the `export PATH` line:

```bash
PATH=/usr/local/share/npm/bin:$PATH
```

Open a new terminal for the `$PATH` changes to take effect.

We also need to tell npm where to find the Xcode Command Line Tools, by running:

    $ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer

Let's install some global packages which we'll use in development:

    $ npm install -g cordova ionic gulp grunt bower webpack browserify

### Npm usage

To install a package:

    $ npm install <package> # Install locally
    $ npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    $ npm install <package> --save

To see what's installed:

    $ npm list # Local
    $ npm list -g # Global

To find outdated packages (locally or globally):

    $ npm outdated [-g]

To upgrade all or a particular package:

    $ npm update [<package>]

To uninstall a package:

    $ npm uninstall <package>

## JSHint
Should already be installed in Atom, but you can install it globally using:

    $npm install -g jshint


## InnerSource
Refer to internal documents for setting up InnerSource.

## SourceTree
Download SourceTree from: https://www.sourcetreeapp.com/

## Github
Download GitHub from: https://desktop.github.com/

## Slack
Download Slack from: https://slack.com/
