# Academic Pages
**Academic Pages is a Github Pages template for academic websites.**

![Academic Pages template example](images/homepage.png "Academic Pages template example")

# Getting Started

1. Register a GitHub account if you don't have one and confirm your e-mail (required!)
1. Click the "Use this template" button in the top right.
1. On the "New repository" page, enter your repository name as "[your GitHub username].github.io", which will also be your website's URL.
1. Set site-wide configuration and add your content.
1. Upload any files (like PDFs, .zip files, etc.) to the `files/` directory. They will appear at https://[your GitHub username].github.io/files/example.pdf.
1. Check status by going to the repository settings, in the "GitHub pages" section

See more info at https://academicpages.github.io/

## Running locally

There are two ways to preview the site on your own machine before pushing to GitHub: natively with Ruby, or with Docker. Pick one.

### Option A: Native Ruby

1. Clone the repository.
1. Install Ruby, Bundler, and Node.js.

    On most Linux distributions and [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/about):
    ```bash
    sudo apt install ruby-dev ruby-bundler nodejs build-essential gcc make
    ```
    On macOS:
    ```bash
    brew install ruby node
    gem install bundler
    ```
1. From the repository root, install the Ruby gems:
    ```bash
    bundle install
    ```
    If this fails with a "permission denied" error writing `Gemfile.lock`, a previous Docker run likely left it owned by `root` — delete it (`rm Gemfile.lock`) and run `bundle install` again.
1. Build and serve the site:
    ```bash
    bundle exec jekyll serve -l -H localhost
    ```
    Then open http://localhost:4000/. The server watches the source files and rebuilds automatically on save.

    On some newer Ruby versions (3.2+), the Liquid templating library pinned by this template's `github-pages` gem calls a method (`tainted?`) that no longer exists, which crashes the build with `undefined method 'tainted?'`. This repo already works around it with a small shim at [`_plugins/ruby_taint_compat.rb`](_plugins/ruby_taint_compat.rb) — it only activates itself when the method is missing, so don't remove it unless you've confirmed your Ruby version doesn't need it.

### Option B: Docker

Working from a different OS, or just want to avoid installing dependencies? Use the provided `Dockerfile` to build a container that runs the site for you if you have [Docker](https://www.docker.com/) installed.

Build the container:

```bash
docker build -t jekyll-site .
```

Run it, serving on http://localhost:4000/:

```bash
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

Note: because `-v $(pwd):/usr/src/app` mounts your repo into the container, and the container runs as `root`, any file Bundler writes at runtime (namely `Gemfile.lock`) will end up owned by `root` on your host — this is what causes the "permission denied" error mentioned in Option A if you switch between the two approaches. `Gemfile.lock` is gitignored, so this never affects what gets committed; if it blocks a native `bundle install` afterward, just delete it.

# Maintenance

Bug reports and feature requests to the template should be [submitted via GitHub](https://github.com/academicpages/academicpages.github.io/issues/new/choose). For questions concerning how to style the template, please feel free to start a [new discussion on GitHub](https://github.com/academicpages/academicpages.github.io/discussions).

This repository was forked (then detached) by [Stuart Geiger](https://github.com/staeiou) from the [Minimal Mistakes Jekyll Theme](https://mmistakes.github.io/minimal-mistakes/), which is © 2016 Michael Rose and released under the MIT License (see LICENSE.md). It is currently being maintained by [Robert Zupko](https://github.com/rjzupkoii) and additional maintainers would be welcomed.

## Bugfixes and enhancements

If you have bugfixes and enhancements that you would like to submit as a pull request, you will need to [fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo) this repository as opposed to using it as a template. This will also allow you to [synchronize your copy](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/working-with-forks/syncing-a-fork) of template to your fork as well.

Unfortunately, one logistical issue with a template theme like Academic Pages that makes it a little tricky to get bug fixes and updates to the core theme. If you use this template and customize it, you will probably get merge conflicts if you attempt to synchronize. If you want to save your various .yml configuration files and markdown files, you can delete the repository and fork it again. Or you can manually patch.

---
<div align="center">
    
![pages-build-deployment](https://github.com/academicpages/academicpages.github.io/actions/workflows/pages/pages-build-deployment/badge.svg)
[![GitHub contributors](https://img.shields.io/github/contributors/academicpages/academicpages.github.io.svg)](https://github.com/academicpages/academicpages.github.io/graphs/contributors)
[![GitHub release](https://img.shields.io/github/v/release/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io/releases/latest)
[![GitHub license](https://img.shields.io/github/license/academicpages/academicpages.github.io?color=blue)](https://github.com/academicpages/academicpages.github.io/blob/master/LICENSE)

[![GitHub stars](https://img.shields.io/github/stars/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io)
[![GitHub forks](https://img.shields.io/github/forks/academicpages/academicpages.github.io)](https://github.com/academicpages/academicpages.github.io/fork)
</div>
