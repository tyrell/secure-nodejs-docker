A light-weight and secure Node and friends Docker base image.

# Build the image

`docker build -t tyrell/secure-nodejs-docker:latest .`


# Install Snyk CLI (if you don't have it installed already)

Follow the instructions at https://docs.snyk.io/snyk-cli/install-the-snyk-cli 

# Scan with Snyk CLI

`snyk container test tyrell/secure-nodejs-docker:latest --file=Dockerfile`

As a best practice, follow the report and update the base image if required. Ideally, the output of your Snyk test scan should look as below.

    ❯ snyk container test tyrell/secure-nodejs-docker:latest --file=Dockerfile

    Testing tyrell/secure-nodejs-docker:latest...

    Organization:      tyrell-cxb
    Package manager:   apk
    Target file:       Dockerfile
    Project name:      docker-image|tyrell/secure-nodejs-docker
    Docker image:      tyrell/secure-nodejs-docker:latest
    Platform:          linux/arm64
    Base image:        node:14.20.0-alpine
    Licenses:          enabled

    ✔ Tested 16 dependencies for known issues, no vulnerable paths found.

    According to our scan, you are currently using the most secure version of the selected base image


# Verify Node and NPM versions

    ❯ docker run tyrell/secure-nodejs-docker npm -v
    6.14.17
    
    ❯ docker run tyrell/secure-nodejs-docker node -v
    v14.20.0