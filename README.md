# Responsive frontend workshop

This workshop is made for students of EPITA - SIGL 2025.

The aim of the workshop is to implement a responsive user interface (UI) for Sotracteur.
To implement it, we will use:

- HTML and CSS only (or SASS/SCSS)
- [NodeJS](https://nodejs.org/en/about/): to be able to use dependencies (other developper's code).

## Step 0: Tools

### IDE

We strongly encourage you to use [Visual Studio Code](https://code.visualstudio.com) for your frontend project.
It's totally free and open source.

You don't have to install any extra plugins for this workshop.

### Install NodeJS

You need to install NodeJS (a.k.a `node`) on your local machine.

Because NodeJS is a tool that evolves fast and has multiple versions, we will use a versionning tool to help us using multiple versions, depending on the project we're working on: [NVM](https://github.com/nvm-sh/nvm) (Node Version Manager)

To install `nvm`, follow instructions in the README of the project: https://github.com/nvm-sh/nvm#installing-and-updating

Once `nvm` is install:

- Create a file `.nvmrc` at the root of your repository with `v21` inside
- Install node v21 using `nvm`: `nvm install v21`

Then, everytime you work on your project, you can type `nvm use` command, and it will switch you to the version inside the `.nvmrc` file.

You can verify if everything is fine by checking node version: `node -v`
and it should output version 19.

### Run your app locally with [`http-server`](https://www.npmjs.com/package/http-server)

Then [`http-server`](https://www.npmjs.com/package/http-server) node modules will server your static files on localhost.

Let's expose your index.html from your previous workshop:

```sh
# Make sure you are using NodeJS version 21.
# If you have nvm; just run nvm use
nvm use
# > `node -v` should output v21.x.x
npx http-server .
```

You should see your app running on [localhost:8080](http://localhost:8080).

Now if you change some elements of your `html` page, you just have to refresh in your browser to see your changes applied. Give it a try.

## Step 1: Create **YOUR** Sotracteur

For this Step, you can refer to the static-template we've created:
[EPITA-SIGL2025-SOCRA/static-template (main)](https://github.com/EPITA-SIGL2025-SOCRA/static-template).

Follow the README and run the template after cloning the template repository somewhere on your machine.

### Create your HTML view

**Objective**: Create only with HTML 5 and CSS 3 **your** "Catalogue" view of Sotracteur.

You **do not** have to respect the same layout as our static-template, but we insist on having the following elements (again you can put them wherever you feel like on the page):

- Keep your html `<title>` to `Socra Group XX` (replacing XX by your group number)
- Main navigation bar with "Catalogue", "Commandes" and "Panier"
- An place where user can filter by french "Communes" or "Around me" by sharing location
- An search result lane where you could see tractors available for renting

The template HTML regroups the kind of element we want to see on the page:
![static-template-screenshot](https://github.com/EPITA-SIGL2025-SOCRA/static-template/blob/main/docs/template.png)

Make it yours!

> Important: it is **only static**. You only create a view where navigation is not active. You only create the view for "Produits"

### Add favicon of your own

**Objective**: Create a small SVG drawing that will be **your** sotracteur's `favicon`.

The `favicon` is the little drawing you can see on the browser tab, next to the title of your web page.

The static-template repo provides [a very simple favicon](https://github.com/EPITA-SIGL2025-SOCRA/static-template/blob/main/favicon.svg).

Create your own `favicon` svg file and add it to your repository. You should add it under a new `public` folder.

Your line inside your `index.html`'s `<head>` element should mention the `public/favicon.svg` structure:

```html
<head>
  <!-- which icon to display on the browser tab -->
  <link rel="icon" type="svg" href="public/favicon.svg" />
  <!-- ... -->
</head>
```

### Adapt your Dockerfile

You should now have more than one `index.html` file.
Don't forget to include all other static files (.css, .png, .jpg ...) in your `Dockerfile` for nginx to serve it.

For instance, let's consider the following repo structure:

```plain
.
├── index.html
├── images
│   └── banner.png
├── public
│   └── favicon.svg
├── README.md
└── styles.css

2 directories, 4 files
```

And your `html` would include `styles.css` like:

```html
<link rel="stylesheet" href="/styles.css" />
```

Then the Dockerfile would be:

```Dockerfile
FROM nginx:1.25.4-alpine

COPY ./index.html /usr/share/nginx/html/index.html
COPY ./styles.css /usr/share/nginx/html/styles.css
COPY ./images /usr/share/nginx/html/images
COPY ./public /usr/share/nginx/html/public
```

Build and run it locally to make sure everything is served correctly.

## Challenge: Make me responsive

Make your version of Sotracteur responsive by adding `@media` queries for the following sizes:

- `@media (max-width: 460px) { ... }`: your menu needs to be usable and without horizontal scroll
- `@media (max-width: 768px) { ... }`: the filter by "Commune" is part is collapsible
- `@media (min-width: 1200px) { ... }`: increase the font-size (you will decide the best ratio)

> Important: do **NOT** forget to add the following metadata in the head of your HTML document:

```html
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <!-- ... -->
</head>
```
