
# Gas price service
Serverless lamba to continously fetch gas prices and store in dynamoDB, as well as providing a REST API for access and offline support.

This example demonstrates how to run a service locally, using the
[serverless-offline](https://github.com/dherault/serverless-offline) plugin. It
provides a REST API to provide ethereum gas prices stored in a DynamoDB. A local DynamoDB instance is provided by the
[serverless-dynamodb-local](https://github.com/99xt/serverless-dynamodb-local)
plugin.


Test your service locally, without having to deploy it first.

## Setup
First install the local dependencies and then kick off the local api and database server.
```bash
npm install
npm run offline
```

## Test service offline
Call the getCosts function locally and navigate to http://localhost:3000/gas to get the data.

```bash
npm run local 
```

Subsequent local invokes should update the cost live from the ethgasstation api.

## Deploy
Set up an additional aws profile under ~/.aws/credentials called gas.
```bash
[gas]
aws_access_key_id = ****************
aws_secret_access_key = ****************
```

Run the deploy script to setup your cloudformation stack.
```bash
npm run deploy 
```
After this is complete you will be provided with a public url and api gateway. Prices will be updated every minute.

To force an update, use the following command:
```bash
npm run invoke 
```

## Cleanup
When done testing, if you'd like to tear down everything, simple run:
```bash
npm run destroy 
```
