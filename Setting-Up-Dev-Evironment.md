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