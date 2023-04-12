# Setting up a development environment

There are a few moving parts to the whole MemoRekall-IIIF ecosystem that need to be configured together before you can start development.

1. [POC Mirador](#poc-mirador)
2. [Mirador Fork and Annotaiton plugin](#mirador-fork-and-annotaiton-plugin)

## POC Mirador

First, you will need to get the global environment running. This is the [POC Mirador](https://gitlab.tetras-libre.fr/iiif/POC-mirador) repo. Clone the repo, then follow the instructions to get it running. This is a summary of the main steps:

1. Create a copy of the `.env.template` file called `.env` and in this new file change the `ANNOTOT_SECRET_KEY_BASE` value to a random string.
2. Install [docker desktop](https://www.docker.com/products/docker-desktop/) on your machine. Open the app, this will ensure that you can easily run the development server later on.
3. Build the project by running `docker-compose build` in the main directory.
4. Run the project by running `docker-compose up`. This should create a _container_ on docker desktop called _poc-mirador_. The first time you do this, you may need to wait a **very long time** before things start working (upwards of 15 minutes).
5. You will know everything is working if you go to [http://localhost:9000/](http://localhost:9000/) in your browser and the Mirador interface opens.
6. You can stop the server running in docker desktop by pressing stop on the _poc-mirador_ container. You can run it again here, subsequently it should be a lot quicker booting up (30 seconds to a minute).

You should now have our version of Mirador running on your machine. You can add manifests and media content to the _www_ folder which will be available at the address `http://localhost:9000/data`.

### TypeError: Failed to fetch

You may get an error in Mirador saying `TypeError: Failed to fetch`. This is because the environment is currently set to open a specific manifest on launch which doesn't exist when you clone the repo. To fix this, in the poc-mirador directory open the `src/index.js` file and comment out the `{ manifestId: 'https://iiif.tetras-libre.fr/data/coeso-deliverable/Manual_Network_Configuration.json' }` object in the `windows` and `catalog` fields of the `config` variable.

## Mirador Fork and Annotaiton plugin

Now that you have the global environment, you need to acces the repos that are our fork of Mirador and our annotation plugin. You will notice that _POC-Mirador_ has two _git submodules_ which refer to these repos: [mirador-video-annotation](https://gitlab.tetras-libre.fr/iiif/mirador-video-annotation) (our fork of Mirador) and [miroaor-annotations](https://gitlab.tetras-libre.fr/iiif/mirador-annotations) (the annotation plugin). You will need to clone these repos that make chan ges to them.

### Development

Once you have cloned the repos, you will need to `npm install` their dependencies. Then, you can `npm start` a development browser which will allow you to quickly view modifications in the browser with hot module reloading. _mirador-video-annotation_ will be at [http://localhost:4444/](http://localhost:4444/) and _mirodor-annotations_ will be at [http://localhost:3000](http://localhost:3000).

### Modifications in the global environment

_POC-Mirador_ refers to a git branch of these repos in it's `package.json` file. You will need to find the `"mirador"` and `"mirador-annotations"` `dependencies` in this file, and change the branch reference at the end of the url's to the name of you branch. 

This will allow you to see your changes when running the _POC-Mirador_ container (note that pulling in changes can make restarting of the server slow on first launch).