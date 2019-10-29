# Project creation

## Requirements before start

Before start you need to have installed [Node](https://nodejs.org/es/) \(&gt;=8.10\) on your machine _**\(it's not required on the server\)**_.

To be sure you have installed Node on your machine, just run:

```bash
node --version
```

If you are on MacOS I recommend you to install it via [Homebrew](https://brew.sh/index_es), if you are in Linux install it via your package manager distribution, or if you are in Windows, install it via their [Homepage](https://nodejs.org/es/).

## Creating an APP

To create an app, I used the command below to start my App called **`todolist`**

> If you don't use Yarn follow [this guide](https://create-react-app.dev/docs/getting-started/) that is quite similar, to create an App

```bash
yarn create react-app todolist
```

![Output of the command to create an App with Yarn](.gitbook/assets/captura-de-pantalla-2019-10-28-a-la-s-7.56.23-p.-m..png)

When the command finish to create your App, as the image above, we gonna see the App File structure.

## App file structure

![](.gitbook/assets/captura-de-pantalla-2019-10-28-a-la-s-9.12.47-p.-m..png)

File README.md

{% tabs %}
{% tab title="Root files" %}
### .gitignore

Git ignore file, to avoid versioning files and paths as **`node_modules`** for example.

{% hint style="info" %}
Generate an specific gitignore file [here](https://www.gitignore.io/).
{% endhint %}

### README.md

Basic README file for git, to help people how can them use your repository.

### package.json

Common js package file which describes your project dependencies and configuration

### yarn.lock

Lock file to registry the dependency tree of your dependencies
{% endtab %}

{% tab title=".git" %}
Empty new repository for Git _**\(git config files\)**_, it can be generated running:

```bash
git init
```
{% endtab %}

{% tab title="node\_modules" %}
Folder where your dependencies will be stored, _**\(this folder should not be versioned with git, since it can be generated automatically with the `package.json` file\)**_.
{% endtab %}

{% tab title="public" %}
Folder where you can found your static files

### index.html

Main **`html`** file that server will return to the client, when they request for your webpage.

### manifest.json

The web app manifest is a simple JSON file that tells the browser about your web application and how it should behave when 'installed' on the user's mobile device or desktop. Having a manifest is required by Chrome to show the Add to Home Screen prompt.

{% hint style="info" %}
[Web App Manifest](https://developers.google.com/web/fundamentals/web-app-manifest)
{% endhint %}

### robots.txt

A robots.txt file tells search engine crawlers which pages or files the crawler can or can't request from your site. This is used mainly to avoid overloading your site with requests**.**

{% hint style="info" %}
[Introduction to robots.txt](https://support.google.com/webmasters/answer/6062608?hl=en)
{% endhint %}
{% endtab %}

{% tab title="src" %}

{% endtab %}
{% endtabs %}



