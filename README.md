# AdonisjsToFlyio

This is an example "hello world" Adonis JS project for deployment to fly.io

## Prerequisites

1. Install [AdonisJS](https://adonisjs.com) as per [the documentation](https://docs.adonisjs.com/guides/installation)
1. Setup a [fly.io](https://fly.io) account

## Setup for deployment

1. Write your Adonisjs code as usual
1. Build the project with `node ace build --production`
1. Setup the project for fly.io: `flyctl launch` in the project root (accept/change the defaults as required)
1. Update the `Dockerfile` - remove the following lines:
```
COPY . .
RUN npm install && npm run build
```
5. Replace with
```
COPY ./build .
COPY ./.env.production ./.env

RUN npm install
```
## Changes implemented

This update makes the following changes:
- uses the `build` directory as the source for the production server's files
- copies the `.env.production` file from the project root to the build root, and renames to `.env`
- removes the build step, as this has aleady been performed by step 2 above
