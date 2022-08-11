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

    ❯ docker run tyrell/secure-nodejs-docker node /app/index.js
        Platform:  linux
        Node version:  v14.20.0
        Node dependencies:  {
            node: '14.20.0',
            v8: '8.4.371.23-node.87',
            uv: '1.42.0',
            zlib: '1.2.11',
            brotli: '1.0.9',
            ares: '1.18.1',
            modules: '83',
            nghttp2: '1.42.0',
            napi: '8',
            llhttp: '2.1.5',
            openssl: '1.1.1q',
            cldr: '40.0',
            icu: '70.1',
            tz: '2021a3',
            unicode: '14.0'
        }

# Next steps

Congratualtions! You have a clean and secure base image. 

Once you start adding your Node.js application and its dependencies to the base image you will still have to ensure both the new image and it's contents are secure. The best way to gurantee compliance is to harden your CI/CD pipeline to include these checks every time a change is commited.
