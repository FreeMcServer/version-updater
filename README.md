# BlockUpdate

[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)

BlockUpdate is a TypeScript app to create a Minecraft version JAR download API.

## Usage

An image is available on DockerHub on: https://hub.docker.com/r/freemcservernet/blockupdate

First Clone the repository and cd into it.

We require docker & docker-compose to use this for simplicity purposes. You can find information on how to download
docker for your platform [here](https://docs.docker.com/get-docker/) and
docker-compose [here](https://docs.docker.com/compose/install/).

Once you have all the tools installed, you can copy the .env.sample file and call it .env, and then add any environment
variables needed for you there. One helpful environment variable is the DEBUG=true one.

Once your environment variables are all setup, run the following command to get all jars (Please note this may take a
while to run!).

```bash
docker-compose up
```

## Env Variables

```properties
DEBUG=false #Only generate sample files and not actual JARs
S3_UPLOAD=false #Enable/Disable S3 Upload
S3_REGION=fr-par #S3 region
S3_ENDPOINT=#S3 endpoint
S3_BUCKET=#S3 bucket name
S3_KEY=#S3 access key
S3_SECRET=#S3 secret key
S3_PULL_BASE=#Base URL of the remote S3 public bucket (to fetch remote versions)
DISCORD_WEBHOOK_ENABLE=false #Notify a discord webhook when we update a version?
DISCORD_WEBHOOK_URL=#Discord webhook URL
```

## S3 Uploading

This system is able to generate local copies of Minecraft JARs locally for local user, but can also be used to generate
and maintain a S3 bucket for automated download by other systems.

To do this you should configure the S3_UPLOAD variable to true, and then configure the S3_* variables.

Please note that an additional directory will be created and used on your bucket, so all contents generated by this
script will be uploaded to `<bucket-root>/jar/`

## Output

The JAR files, along with its metadata will be generated on the /out directory.

Using the following format:

```
./out
├── spigot
├────── 1.14.4
├────────── spigot-1.14.4.jar
├────────── build.txt
├────────── version.json
├────── versions.json
```

There will be a directory with the name of the version, inside this directory will be a file called `build.txt` (with the
current build number for the JAR on the same folder), and a file called _variant_-_version_.jar with the version specific JAR
file. There will also be a versions.json file with all the versions available along with some metadata for each version. The version.json inside the version folder will also contain the same version metadata.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

[GPL-3.0-or-later](https://choosealicense.com/licenses/gpl-3.0/)

## Authors

- [@SpaceQuacker](https://github.com/Bombardier-C-Kram)
- [@facha](https://github.com/nfacha)
- [@Alvinn8](https://github.com/Alvinn8)
