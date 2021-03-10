---
title: "CI"
---

The CI task enables almost any action in your pipeline by pulling a specific Docker image from a registry endpoint, and deploying it to a Docker host. It then executes the configured script in the context of the running container.

The CI task runs using parameters configured in the [Pipeline](/Pipelines) Workspace configuration, including the Container Image, Docker Registry, Docker Host, directory, cache, environment variables and CPU/Memory limits.

## Inputs

