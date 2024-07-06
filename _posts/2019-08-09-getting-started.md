---
title: Getting Started
description: >-
  Get started with Chirpy basics in this comprehensive overview.
  You will learn how to install, configure, and use your first Chirpy-based website, as well as deploy it to a web server.
author: cotes
date: 2019-08-09 20:55:00 +0800
categories: [Blogging, Tutorial]
tags: [getting started]
pin: true
media_subpath: '/posts/20180809'
---

## Creating a New Site

There are two ways to create a new repository for **Chirpy**:

- [**Using the Starter**](#option-1-using-the-starter) — This method makes upgrades easy and isolates irrelevant project files, allowing you to focus on writing.
- [**Forking the Theme**](#option-2-forking-the-theme) — This method is convenient for custom development but challenging to upgrade. Unless you are familiar with Jekyll and plan to tweak or contribute to this project, this approach is not recommended.

### Option 1: Using the Starter

1. Sign in to GitHub and navigate to the [**Starter**][starter].
2. Click the <kbd>Use this template</kbd> button and then select <kbd>Create a new repository</kbd>.
3. Name the new repository `USERNAME.github.io`, where `USERNAME` is your GitHub username.

### Option 2: Forking the Theme

1. Sign in to GitHub and [fork the Theme](https://github.com/cotes2020/jekyll-theme-chirpy/fork).
2. Rename the new repository to `USERNAME.github.io`, where `USERNAME` is your GitHub username.

## Setting Up the Environment

The easiest way to set up the runtime environment, especially on Windows, is by using [Dev Containers](#setting-up-in-dev-containers). This method installs all packages within a Docker container, isolating them from the host machine and ensuring no interference with existing settings.

For Unix-like systems, besides using Dev Containers, you can also [natively set up](#setting-up-natively) the runtime environment to achieve optimal performance.

### Setting Up in Dev Containers

1. Install Docker:
   - On Windows/macOS, install [Docker Desktop][docker-desktop].
   - On Linux, install [Docker Engine][docker-engine].
2. Install [VS Code][vscode] and the [Dev Containers extension][dev-containers].
3. Clone your repository:
   - For Docker Desktop: Start VS Code and [clone your repo in a container volume][dc-clone-in-vol].
   - For Docker Engine: Clone your repo to the local disk, then launch VS Code and [open your repo in the container][dc-open-in-container].
4. Wait a few minutes for Dev Containers to finish installing.

### Setting Up Natively

1. Follow the instructions in the [Jekyll Docs](https://jekyllrb.com/docs/installation/) to complete the installation of the basic environment. Ensure that [Git](https://git-scm.com/) is also installed.
2. Clone your repository to a local disk.
3. If your site was created by forking the main repository, install [Node.js][nodejs] and run `bash tools/init.sh` in the repo root directory to initialize files.
4. Install the dependencies by running `bundle`.

### Start the Jekyll Server

To run the site locally, use the following command:

```console
$ bundle exec jekyll s
```

After a few seconds, the local server will be available at <http://127.0.0.1:4000>.

## Usage

### Configuration

Update the variables in `_config.yml`{: .filepath} as needed. Some typical options include:

- `url`
- `avatar`
- `timezone`
- `lang`

### Social Contact Options

Social contact options are displayed at the bottom of the sidebar. You can enable or disable specific contacts in the `_data/contact.yml`{: .filepath} file.

### Customizing the Stylesheet

To customize the stylesheet, copy the theme's `assets/css/jekyll-theme-chirpy.scss`{: .filepath} file to the same path in your Jekyll site, and add your custom styles at the end of the file.

Starting with version `6.2.0`, if you want to overwrite the SASS variables defined in `_sass/addon/variables.scss`{: .filepath}, copy the main SASS file `_sass/main.scss`{: .filepath} to the `_sass`{: .filepath} directory in your site's source, then create a new file `_sass/variables-hook.scss`{: .filepath} and assign your new values there.

### Customizing Static Assets

Static assets configuration was introduced in version `5.1.0`. The CDN of the static assets is defined in `_data/origin/cors.yml`{: .filepath }. You can replace some of them based on the network conditions in the region where your website is published.

If you prefer to self-host the static assets, refer to the [_chirpy-static-assets_](https://github.com/cotes2020/chirpy-static-assets#readme) repository.

## Deployment

Before deploying, check the `_config.yml`{: .filepath} file and ensure the `url` is configured correctly. If you prefer a [**project site**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) and don't use a custom domain, or if you want to visit your website with a base URL on a web server other than **GitHub Pages**, remember to set the `baseurl` to your project name, starting with a slash, e.g., `/project-name`.

Now you can choose _ONE_ of the following methods to deploy your Jekyll site.

### Deploy Using GitHub Actions

Prepare the following:

- If you're on the GitHub Free plan, keep your site repository public.
- If you have committed `Gemfile.lock`{: .filepath} to the repository, and your local machine is not running Linux, update the platform list of the lock file:

  ```console
  $ bundle lock --add-platform x86_64-linux
  ```

Next, configure the _Pages_ service:

1. Go to your repository on GitHub. Select the _Settings_ tab, then click _Pages_ in the left navigation bar. In the **Source** section (under _Build and deployment_), select [**GitHub Actions**][pages-workflow-src] from the dropdown menu.  
   ![Build source](pages-source-light.png){: .light .border .normal w='375' h='140' }
   ![Build source](pages-source-dark.png){: .dark .normal w='375' h='140' }

2. Push any commits to GitHub to trigger the _Actions_ workflow. In the _Actions_ tab of your repository, you should see the workflow _Build and Deploy_ running. Once the build is complete and successful, the site will be deployed automatically.

You can now visit the URL provided by GitHub to access your site.

### Manual Build and Deployment

For self-hosted servers, you will need to build the site on your local machine and then upload the site files to the server.

Navigate to the root of the source project, and build your site with the following command:

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

Unless you specified the output path, the generated site files will be placed in the `_site`{: .filepath} folder of the project's root directory. Upload these files to your target server.

[nodejs]: https://nodejs.org/
[starter]: https://github.com/cotes2020/chirpy-starter
[pages-workflow-src]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow
[docker-desktop]: https://www.docker.com/products/docker-desktop/
[docker-engine]: https://docs.docker.com/engine/install/
[vscode]: https://code.visualstudio.com/
[dev-containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[dc-clone-in-vol]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume
[dc-open-in-container]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container
