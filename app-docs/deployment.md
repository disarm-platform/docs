# App: Deployment manual

This document describes deployment of the combination of three DiSARM services: [app \(v2\)](https://github.com/disarm-platform/disarm-app/tree/develop-2.x), [editor](https://github.com/disarm-platform/disarm-editor/tree/develop), and [server \(v8\)](https://github.com/disarm-platform/disarm-server/tree/develop-v8).

## Prerequisites:

Server running with:

* [Git](https://git-scm.com/downloads)
* [MongoDB](https://www.mongodb.com/download-center/community)
* [NodeJS](https://nodejs.org/en/download/)
* Web server \(examples below use an opern source version of [Caddy](https://github.com/disarm-platform/disarm-editor/tree/develop)\)

## Overview

It’s possible to deploy the services almost anywhere, so long as the app and editor are configured to point to the server’s URL, and the two frontend services are available via HTTPS \(required for browser functionality\). Configuration of the DNS and web servers, etc is not covered in these instructions.

The `README.md` in each repo contains more detailed instructions for each service.

## Deploy disarm-server

1. Clone the repo: `git clone https://github.com/disarm-platform/disarm-server`
2. Checkout the `develop-v8` branch
3. Install dependencies
4. Configure DNS
5. Start server running \(consult `README.md`\) for info and options: e.g. `SECRET=secret MONGODB_URI=mongodb://localhost:27017 PORT=3001 npm start`

## Deploy disarm-app

1. Clone the repo: `git clone https://github.com/disarm-platform/disarm-app`
2. Checkout the `develop-v2.x` branch
3. Edit the server URL property in `src/config/common.js` to point to the configured server above
4. Install dependencies: `npm install`
5. Build the app: `npm run build`
6. Configure DNS

## Deploy disarm-editor

1. Clone the repo: `git clone https://github.com/disarm-platform/disarm-editor`
2. Checkout the `develop` branch
3. Edit the server URL property in `src/lib/common.ts` to point to the configured server above
4. Install dependencies: `npm install`
5. Build the app: `npm run build`
6. Configure DNS

## Example Caddy config

```text
# app
app.example.com {
        root disarm-app/dist
        rewrite / {
                ext /
                to {path} /index.html
        }
        timeouts {
                read 1m
        }
        log access.log
        gzip
}

# editor
editor.example.com {
        root disarm-editor/dist
        rewrite / {
                ext /
                to {path} /index.html
        }
        timeouts {
                read 1m
        }
        log access.log
        gzip
}
```

