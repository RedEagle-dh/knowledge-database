# Github

## Github Actions

### Deployment with docker

If you deploy a Next.js project based on Node v20 and struggle with environment variables, here you find your answers!

First you'll need a .github/workflows/docker-image.yml file in your project's root folder.

This could be it:

```yml
name: Docker Image CI

on:
    push:
        branches: ["master"]
    pull_request: {
        branches: ["master"]
    }

jobs:
    build-and-push:
        runs-on: ubuntu-latest
        environment: production
        permissions:
            contents: read
            packages: write

        steps:
            - uses: actions/checkout@v4

            - name: Set up Docker Buildx
              uses: docker/setup-buildx-action@v3

            - name: Login to DockerHub
              uses: docker/login-action@v3
              with:
                  username: ${{ secrets.DOCKERHUB_USERNAME }}
                  password: ${{ secrets.DOCKERHUB_TOKEN }}

            - name: Build and push Docker image
              uses: docker/build-push-action@v5
              with:
                  push: true
                  tags: username/repository:TAG
                  build-args: |
                      SECRETONE=${{ secrets.SECRETONE }}
                      SECRETTWO=${{ secrets.SECRETTWO }}
```

So the github action will start if you push a new commit to master or make a PR to master.
The action will create a docker image and automatically tag it and push it to the docker hub.
So you need to create `repository secrets` in your repository on github. You find them in the settings in your repo under `Security > Secrets and variables > Actions`.
There you create DOCKERHUB_TOKEN and DOCKERHUB_USERNAME. You get both from your docker account settings.

If you want to have environment secrets e.g. `NEXT_PUBLIC_URL` which you need in a Next.js project, you have to add them with `build-args`.
You need to add the secrets for that in the environment secrets at the same page like the repository secrets.
You just have to declare these secrets in the Dockerfile after `COPY . .` and before `RUN npm run build`:

```dockerfile
ARG SECRETONE
ARG SECRETTWO

ENV SECRETONE=${SECRETONE}
ENV SECRETTWO=${SECRETTWO}
```

It's not recommended to add every secret like that, because you can find these secrets in the docker image later. If you can add secrets during runtime (e.g. if you use Doppler Secrets), do so.

