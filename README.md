# API Docs
Documentation of our *public* API to be used by our partners

Deployed at [https://engineering.unmade.com/api-docs/](https://engineering.unmade.com/api-docs/).

Rendered using [Blueprinter](https://github.com/funbox/blueprinter/)

## Local Development

Start the dev server:

```shell
docker-compose up dev
```

You can then navigate to [http://localhost:3000/](http://localhost:3000/)
to see a live preview.

## Deployment

When you've made your changes to the `apiary.apib` file, just push any changes
to the `main` branch and the pages site will be automatically updated via a
GitHub action.
