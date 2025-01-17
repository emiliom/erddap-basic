# ERDDAP basics

This repo will help you get started getting a dataset into ERDDAP. It includes a demonstration dataset.

We will install using Docker, which installs ERDDAP into a 'container' on your computer, and avoids the need for you to install and configure all the components that ERDDAP relies on to work, such as Java, Apache, and Tomcat.

## Setup

- Install [docker](https://docs.docker.com/install/) and [docker-compose](https://docs.docker.com/compose/install/). Depending on your operating system, docker-compose may come with Docker
- `cd` into the directory of this git repo and run `docker-compose up`. This may take a while to run the first time as it needs to dowload the Docker images
- See if it works by going to http://localhost:8070/erddap

## Configuring

 - put your data files (eg .nc or .csv files) into a new folder in the 'datasets' folder.

 - Run `sh GenerateDatasetsXml.sh` in the terminal from this directory:
    - use `EDDTableFromAsciiFiles` for .csv files and `EDDTableFromMultidimNcFiles` for netCDF (.nc) files.
    - 'Starting directory' is your new directory where your files are located, eg: /datasets/sample-dataset
    - 'File name regex' use '.*' (without the quotes) to match all files in this directory

  If this was successful, it will create a snippet which is output to bigParentDirectory/logs folder as well as to the screen. Paste that snipped into the file `config/datasets.xml`

 - `datasets.xml` is where the datasets are configured. There are too many options to list here, see https://coastwatch.pfeg.noaa.gov/erddap/download/setupDatasetsXml.html for help. Once you have edited it to your liking, make note of the datasetID you are working on.

- To test your configuration, run `sh DasDds.sh` and then type in your dataset ID when prompted.

After a change is made to a dataset, you can either restart erddap with
`docker-compose restart`, or reload just that dataset by running
`sh reload_dataset <your-dataset-id-here>`:

## Restarting

- Use `docker-compose restart` for this. You _shouldn't_ need to use this for dataset changes but sometimes it helps.

## Stopping

`docker-compose down`

## Troubleshooting

- See http://localhost:8070/erddap/status.html for status
- See `bigParentDirectory/logs/log.txt` for more information
- Test your dataset with the `DasDds.sh` script
