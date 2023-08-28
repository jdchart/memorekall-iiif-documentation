# POC Mirador (global environment)

Let's take a closer look at the [POC Mirador](https://gitlab.tetras-libre.fr/iiif/POC-mirador) repo. Thsi is the global environment that brings all of the various moving parts together, and simulates an instance of MemoRekall-IIIF on a server.

1. [Configuration](#configuration)
2. [Repo hierarchy](#repo-hierarchy)

## Configuration

The repo is a [node.js](https://nodejs.org/en) package, meaning that it has the typical `package.json` file, a `node_modules` folder etc. As explained on the [Setting up a development enviropment](/development-guide/01-Setting-Up-Dev-Evironment.md) page, when you clone the repo, you first start by copying the `.env.template` file under the new name `.env`, and building the docker container.

## Repo hierarchy

Let's have a look at the contents of the repo:

```
├── .gitignore
├── README.md

├── node_modules
├── package.json
├── package-lock.json

├── annotations-plugin
├── mirador-video-annotation
├── .gitmodules

├── www

├── annotot-db

├── src
│   ├── index.js
│   ├── catalog.js

├── public
│   ├── index.html



├── .dockerignore
├── .env
├── .env.template
├── docker-compose.yml
├── Dockerfile





├── traefik.yml
├── webpack.config.js
├── dev.yml
├── Caddyfile
```

### .gitignore and README.md

These are the basic [git](https://git-scm.com/) repo files. `.gitignore` tells git which folders and files to ignore (they stay on your local machine) and the `README.md` file is a markdown file giving basic information about the repo and instructions on how to get it running.

### node_modules, package.json and package-lock.json

There pertain to the [node.js](https://nodejs.org/en) package. The `node_modules` folder is where all of the dependencies will be installed (note that this is ignored by git, making the repo more lightweight).

The `package.json` file gives metadata about the node package (name, version, description etc.). It also give a list of `dependencies` - other node packages that are required to get the package to work.

The `package-lock.json` file is similar to `package.json`: it's main function is to ensure that the versions of the various dependencies are buiult in  the same way when people will clone the repo. For more precise information on the differences between package and package-lock see [this page](https://www.geeksforgeeks.org/difference-between-package-json-and-package-lock-json-files/).

### annotations-plugin, mirador-video-annotation and .gitmodules

The `annotations-plugin` and `mirador-video-annotation` are [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules). These are the references to two other git repos.

[mirador-video-annotation](https://gitlab.tetras-libre.fr/iiif/mirador-video-annotation) is the repo of our fork of Mirador.

[mirador-annotations](https://gitlab.tetras-libre.fr/iiif/mirador-annotations) is the repo of our annotation plugin for Mirador.

These are the modules to modify if you wish to make changes to the interface and underlying systems. There are dedicated pages to each of these modules in this guide.

The `.gitmodules` file is a file that tells git about these modules and where to find them. Like node packages, this system allows the repo to be lighterweight, and the submodules will be downloaded and installed on your local machine during setup of the package.

### www

This is an empty folder where you will be able to put content that will be available at the path `http://localhost:9000/data`. It is where you will store media and manifests for testing. You can create your own folder hierarchy within this folder. Note that you will also be able to refer to media and data stored elsewhere as long as you have permission.

### annotot-db

This is will be used to make persistant annotations when creating new annotations. Annotatot provides a simple [RESTful endpoint](https://restfulapi.net/) (GET, POST, DELETE http requests) for persisting annotations. For more information, have a look at their [documentation](https://github.com/PenguinParadigm/annotot). Think of it as a server that stores all of the new annotation data. The `annotot-db` folder is automatically created.

