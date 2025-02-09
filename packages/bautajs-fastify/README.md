## bautajs-fastify

A Fastify plugin for Bauta.js.

## How to install

```console
  npm install @axa/bautajs-fastify
```

## Usage

```js
const { bautajsFastify } = require('@axa/fastify');
const fastify = require('fastify')();
const apiDefinition = require('../../api-definition.json');

fastify.register(bautajsFastify, {
  apiDefinition,
  resolversPath: './glob-path-to-your-resolvers/*.js',
  staticConfig: {
    someVar: 2
  }
});

fastify.listen(3000, err => {
  if (err) throw err;
  fastify.log.info('Server listening on localhost:', fastify.server.address().port);
});

```
## Features


### Fastify included plugins

By default the following plugins are included on the fastify instance

- [@fastify/swagger](https://github.com/fastify/fastify-swagger) - Automatic swagger documentation exposed through the `${prefix}/explorer` path.

### Serialization

[Fastify response serialization](https://github.com/fastify/fastify/blob/main/docs/Validation-and-Serialization.md#serialization) is enabled by default if a response schema is provided, so this means that missing properties from the schema will not be returned on the response. Although, this behaviour can be disabled by the setting `strictResponseSerialization` set to false.

### Validation

### Request validation

Fastify has an out-of-the-box request validation, since this validation takes place first, any error in the schema validation will be generated by fastify and not by `bautajs-core`. Therefore, even if you disable the validation of the request using the [bautajs-core methods](https://github.com/axa-group/bauta.js/blob/main/docs/validation.md#request-validation), the fastify validation will take place anyway.

### Response validation

The response validation of `bautajs-fastify` is related to the flag `strictResponseSerialization`. If this is enabled (is the default behaviour), **the fastify response validation will be used**.

This happens because the response schema is used to create the fastify route related to the OpenAPI operation identifier. Since this validation takes place first, any error in the schema validation will be generated by fastify and not by `bautajs-core`.

If you want to use the validation mechanism of `bautajs-core` (see [Bauta.js validation](https://github.com/axa-group/bauta.js/blob/main/docs/validation.md), you must disable the `strictResponseSerialization` flag.

# Legal Notice

Copyright (c) AXA Group. All rights reserved.
Licensed under the (MIT / Apache 2.0) License.
# Third party dependencies licenses

## Production
 - [@axa/bautajs-core@5.1.0](git+https://github.com/axa-group/bauta.js) - MIT*
 - [fastify@4.5.2](https://github.com/fastify/fastify) - MIT
 - [@fastify/swagger@7.4.1](https://github.com/fastify/fastify-swagger) - MIT
 - [fastify-plugin@4.2.1](https://github.com/fastify/fastify-plugin) - MIT
 - [fastify-x-request-id@2.0.0](https://github.com/dimonnwc3/fastify-x-request-id) - MIT
 - [route-order@0.1.0](https://github.com/sfrdmn/node-route-order) - MIT

## Development
 - [@axa/bautajs-datasource-rest@5.1.2](https://github.com/axa-group/bauta.js) - MIT*

## Third party dependencies licenses

### Production
 - [@axa/bautajs-core@1.0.0](https://github.com/axa-group/bauta.js) - MIT*
 - [fastify@4.5.3](https://github.com/fastify/fastify) - MIT
 - [@fastify/swagger@7.4.1](https://github.com/fastify/fastify-swagger) - MIT
 - [fastify-plugin@4.2.1](https://github.com/fastify/fastify-plugin) - MIT
 - [route-order@0.1.0](https://github.com/sfrdmn/node-route-order) - MIT

### Development
 - [@axa/bautajs-datasource-rest@1.0.0](https://github.com/axa-group/bauta.js) - MIT*
