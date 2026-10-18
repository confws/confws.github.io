# ConfWS website

> The website for the 29th International Workshop on Configuration (ConfWS'27)

---

## What is this?

This is a Jekyll-based website for the ConfWS workshop. This repository comprises templates and files with the content. The real website is generated from these files using the [Jekyll static-website generator](https://jekyllrb.com) and the [minimal mistakes template](https://mmistakes.github.io/minimal-mistakes).

The ConfWS website is deployed in [Github Pages](https://pages.github.com/). Authors can create new content using [Prose](http://prose.io/), [Netlify](https://www.netlify.com/) or the [Github](https://github.com) web interface. This repository must be cloned/forked only for development.

This site is inspired in [AcademicPages/events](https://github.com/academicpages/events), a fork from the [minimal mistakes template](https://mmistakes.github.io/minimal-mistakes). 

## Local installation for development

You can install Jekyll on your computer to preview the changes before pushing them to the Github repository. 

The following are instructions for Ubuntu Linux (or Ubuntu/WSL on Windows 10)

1. Install Jekyll pre-requisites, including the Ruby language

   ```
   sudo apt-get install ruby-full build-essential zlib1g-dev
   ``` 

2. Configure the Ruby language to install software in the `$HOME` directory 

   ```
   echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
   echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
   echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
   source ~/.bashrc
   ``` 

3. Install Jekyll

   ```
   gem install jekyll bundler
   ``` 

3. Download the website

   ```
   git clone https://github.com/confws/confws.github.io.git
   ``` 

4. Install additional libraries required by Jekyll

   ```
   cd confws.github.io
   bundle install
   ``` 

5. Run the Jekyll preview to preview and regenerate the website when the files are changed

   ```
   bundle exec jekyll serve
   ``` 

5. Preview the site using a web browser

   ```
   http://localhost:4000
   ``` 
   
## Yearly rollover

This repository (`confws.github.io`, served at https://confws.github.io/) always hosts the **current** edition. Past editions are archived in one repository per year (`confws/2023`, `confws/2024`, ...), served at `https://confws.github.io/<year>/`. When a new edition starts:

1. Create the archive repository and mirror this one into it:

   ```
   gh repo create confws/<year> --public --description "<Nth> International Workshop on Configuration (ConfWS'<yy>)"
   git clone --bare git@github.com:confws/confws.github.io.git
   cd confws.github.io.git && git push --mirror git@github.com:confws/<year>.git
   ```

2. In the archive, set `url: https://confws.github.io/<year>` and `repository: confws/<year>` in `_config.yml` (leave `baseurl` empty, GitHub Pages sets it), and replace links to `https://confws.github.io/assets/...` with `https://confws.github.io/<year>/assets/...`.
3. Enable GitHub Pages for the archive (branch `main`, folder `/`):

   ```
   gh api -X POST repos/confws/<year>/pages -f 'source[branch]=main' -f 'source[path]=/'
   ```

4. Once `https://confws.github.io/<year>/` is live, update this repository for the new edition and add the archived edition to `_pages/history.md`.

---

### Licenses

This website uses the [Minimal Mistakes Jekyll Theme](https://mmistakes.github.io/minimal-mistakes) that is licensed using [The MIT License (MIT)](https://opensource.org/licenses/MIT).