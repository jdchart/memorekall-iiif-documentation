# POC Mirador (global environment)

Let's take a closer look at the [POC Mirador](https://gitlab.tetras-libre.fr/iiif/POC-mirador) repo. Thsi is the global environment that brings all of the various moving parts together, and simulates an instance of MemoRekall-IIIF on a server.

## Configuration

The repo is a [node.js](https://nodejs.org/en) package, meaning that it has the typical `package.json` file, a `node_modules` folder etc. As explained on the [Setting up a development enviropment](/development-guide/01-Setting-Up-Dev-Evironment.md) page, when you clone the repo, you first start by `npm install`ing the dependencies for the package. This will download and install different node packages putting them in the `node_modules` folder.

Let's have a look at the contents of the repo:

```
├── node_modules

├── annotations-plugin
├── mirador-video-annotation
├── .gitmodules

├── annotot-db

├── src
│   ├── index.js
│   ├── catalog.js

├── public
│   ├── index.html

├── www

├── .dockerignore
├── .env
├── .env.template
├── docker-compose.yml
├── Dockerfile

├── package-lock.json
├── package.json

├── .gitignore
├── README.md

├── traefik.yml
├── webpack.config.js
├── dev.yml
├── Caddyfile
```