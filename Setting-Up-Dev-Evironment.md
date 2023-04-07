# Setting up a development environment

There are a few moving parts to the whole MemoRekall-IIIF ecosystem that need to be configured together before you can start development.

## POC Mirador

First, you will need to get the global environment running. This is the [POC Mirador](https://gitlab.tetras-libre.fr/iiif/POC-mirador) repo. Clone the repo, then follow the instructions to get it running. These are the main steps:

- Create a copy of the `.env.template` file called `.env` and in this new file change the `ANNOTOT_SECRET_KEY_BASE` value in this file to a random string.
- Install [docker desktop](https://www.docker.com/products/docker-desktop/) on your machine. Open the app, this will ensure that you can easily run the development server later on.
- Build the project by running `docker-compose build` in the main directory.
- Run the project by running `docker-compose up`. This should create a _container_ on docker desktop called _poc-mirador_. The first time you do this, you may need to wait a **very long time** before thigns start working (upwards of 15 minutes).
- You will know everything is working if you got to [http://localhost:9000/](http://localhost:9000/) in your browser and the Mirador interface opens.
- You can stop the server running in docker desktop by pressing stop on the _poc-mirador_ container. You can run it again here, subsequently it should be a lot quicker booting up (30 seconds to a minute).

You may get an error in Mirador saying `TypeError: Failed to fetch`. This is because the environment is currently set to open a specific manifest on open which doesn't exist whern you clone the repo. To fix this, in the poc-mirador directory open the `src/index.js` file and comment out the `{ manifestId: 'https://iiif.tetras-libre.fr/data/coeso-deliverable/Manual_Network_Configuration.json' }` object in the `windows` and `catalog` fields of the `config` variable.

You should now have our version of Mirador running on your machine. You can add manifests and media content to the _www_ folder which will be available at the address `http://localhost:9000/data`.

## Mirador Fork

Next, if you wish to make modifications to our fork of Mirador, you will need to clone the [mirador-video-annotation](https://gitlab.tetras-libre.fr/iiif/mirador-video-annotation) repo. 

Go to this directory and `npm install` it's dependencies, and run `npm start` to run the devleopment browser. This will run at [http://localhost:4444/](http://localhost:4444/). We recommend actively developing on this server before pushing changes.

To bring these changes into the POC-mirador repo, you will need to make a new branch in the mirador-video-annotation, and reference this branch. To do this, go to the `package.json` file in poc-mirador, find the `"mirador"` `dependency`, and chnage the branche reference at the end of the url from `annotation-on-video` to your branch name.

Now if you restart the server, the changes you commited on your development branch should apprear.

## Annotation plugin

The final part of the ecosystem is our fork of the annotations plugin which is found in the [mirodor-annotations](https://gitlab.tetras-libre.fr/iiif/mirador-annotations) repo. Like the mirador fork, you will need to clone this repo and create your own branch. 