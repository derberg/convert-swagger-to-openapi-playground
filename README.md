# Convert Swagger to OpenAPI Playground

Staying with Swagger 2.0 is like staying with ... still working on a good comparison. Anyway, you should migrate to OpenAPI, and my goal here is not to convince you why. I assume you already made this smart decision, and I just want to make it easier for you.

I did not perform any more in-depth investigation of available tools. There are [tools](https://github.com/Mermade/oas-kit) provided by Mermade Software. To be more specific, by [Mike Ralphson](https://twitter.com/PermittedSoc) that is a member of [Technical Steering Committee](https://github.com/OAI/OpenAPI-Specification/blob/master/MAINTAINERS.md). For me, this is a good reason not to research different tools.

- [Convert in a Browser](#convert-in-a-browser)
- [Convert in a Terminal](#convert-in-a-terminal)
    - [NPM](#npm)
    - [NPX](#npx)
    - [Docker](#docker)
- [Convert Multiple Files](#convert-multiple-files)

## Convert in a Browser

Conversion in a browser is addressed by [Kin Lane](https://twitter.com/kinlane) aka API Evangelist in [this thread and the video](https://twitter.com/apievangelist/status/1295502093625643008) so watch it and go to https://mermade.org.uk/openapi-converter

## Convert in a Terminal

Use [swagger2openapi](https://github.com/Mermade/oas-kit/blob/master/packages/swagger2openapi/README.md) and have fun:

### NPM

1. Install the tool `npm install -g swagger2openapi`
1. Run conversion `swagger2openapi --yaml --outfile openapi.yaml https://petstore.swagger.io/v2/swagger.json`

And that is it. Check your new `openapi.yaml` file.

### NPX

[NPX](https://www.npmjs.com/package/npx) is useful in CI/CD where you do not want to install `swagger2openapi` globally.

`npx -p swagger2openapi swagger2openapi --yaml --outfile openapi.yaml https://petstore.swagger.io/v2/swagger.json`

### Docker

NPM and NPX is not your thingy? use the Docker image provided by Mike.

```bash
#this part "-v ${PWD}:/usr/src/app" mounts the directory where you started "docker run" inside the container where CLI is triggered, this way generated "openapi.yaml" gets into your local drive
docker run --rm -v ${PWD}:/usr/src/app mermade/swagger2openapi swagger2openapi --yaml --outfile openapi.yaml https://petstore.swagger.io/v2/swagger.json
```

## Convert Multiple Files

You most probably have many services, and you need to convert many Swagger files, and you do not want to do it one by one but all at once with a script. You can use Bash and write some script that runs the CLI, but writing Bash scripts is like ... yeah, one day I'll find a good comparison.

Just use `swagger2openapi` as a library. In `convertmultiple` directory, you can find a [sample code](convertmultiple/index.js) that you can easily edit for your needs. Its code has proper comments that will help you understand what parts you might change in case you have different directory structure or filenames than the ones used in the sample

To play with the example, perform the following steps:
1. `git clone https://github.com/derberg/convert-swagger-to-openapi-playground.git`
1. `cd convert-swagger-to-openapi-playground/convertmultiple`
1. `npm install`
1. `npm start`
