
<p align="center">API Documentation for Validar</p>

<p align="center"><img src="https://raw.githubusercontent.com/lord/img/master/screenshot-slate.png" width=700 alt="Screenshot of Example Documentation created with Slate"></p>

<p align="center"><em>The example above was created with Slate. Check it out at <a href="https://lord.github.io/slate">lord.github.io/slate</a>.</em></p>

Setup
------------------------------

### Prerequisites

You're going to need:

 - **Linux or macOS** — Windows may work, but is unsupported.
 - **Ruby, version 2.3.1 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

1. `git clone git@github.com:Evanta/validar-api-docs.git`
2. `cd validar-api-docs`
3. Initialize and start the project. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567. Whoa! That was fast!

Weird open ssl errors?
```
brew install openssl
rvm reinstall ruby-<INSERT RUBY VERSION HERE> --with-openssl-dir=`brew --prefix openssl`
```

### Note on JavaScript Runtime

For those who don't have JavaScript runtime or are experiencing JavaScript runtime issues with ExecJS, it is recommended to add the [rubyracer gem](https://github.com/cowboyd/therubyracer) to your gemfile and run `bundle` again.

### Publishing Your Docs to GitHub Pages
Publishing your API documentation couldn't be more simple.

1. Make sure you're working on a fork in your own account, not the Slate original repo: `git remote show origin.`
2. Commit your changes to the markdown source: `git commit -a -m "Update index.html.md"`
3. Push the markdown source changes to GitHub: `git push`
4. Run `./deploy.sh`

_NOTE: You should not make changes to your repo on github.com._

After you deploy if you make changes to the repo follow these steps:

1. Make sure you're working on a fork in your own account, not the Slate original repo: `git remote show origin.`
2. Commit your changes to the markdown source: `git commit -a -m "Update index.html.md"`
3. Push your changes to github: `git push origin master`
4. Go to the gh-pages branch: `git checkout gh-pages`
5. Bring gh-pages up to date with master: `git rebase master`
6. Commit the changes: `git push origin gh-pages`
7. Return to the master branch to begin new fun! `git checkout master`

--------------------
#### Slate Contributors & Thanks

Slate was built by [Robert Lord](https://lord.io) while interning at [TripIt](https://www.tripit.com/).

Thanks to the following people who have submitted major pull requests:

- [@chrissrogers](https://github.com/chrissrogers)
- [@bootstraponline](https://github.com/bootstraponline)
- [@realityking](https://github.com/realityking)
- [@cvkef](https://github.com/cvkef)

Also, thanks to [Sauce Labs](http://saucelabs.com) for sponsoring the development of the responsive styles.

- [Middleman](https://github.com/middleman/middleman)
- [jquery.tocify.js](https://github.com/gfranko/jquery.tocify.js)
- [middleman-syntax](https://github.com/middleman/middleman-syntax)
- [middleman-gh-pages](https://github.com/edgecase/middleman-gh-pages)
- [Font Awesome](http://fortawesome.github.io/Font-Awesome/)
