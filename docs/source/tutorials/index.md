# Tutorials

These step-by-step tutorials show you how to use various features of Chalice.
These are perfect if you're new to Chalice and want to learn what Chalice can
do. If you want more complete, real-world examples, you can check out
our [Sample Applications](../samples/index.md).

## Rest API Tutorials

[REST API Tutorial](basicrestapi.md)

: This tutorial walks you through creating a REST API in
  Chalice. It covers features such as routing, URL parameters, error handling,
  etc.

[Custom Domain Names](customdomain.md)

: In this tutorial, we show you how to configure
  a REST API with your own custom domain name.

<a id="websocket-tutorial"></a>
## Websocket Tutorials

[Echo Server Example](wsecho.md)

: Learn the basics of creating websocket APIs in Chalice. This tutorial
  creates an echo server that echoes back any message that the client sends to
  the websocket server.

[Chat Server Example](wschat.md)

: In this more complete example, learn how to create a basic chat application
  based on websockets.

## Event Source Tutorials

[Event Sources Tutorial](events.md)

: This tutorial shows you how to create an event handler
  that's triggered whenever a message is published to an SNS topic.

:hidden:
:glob:

*

## AWS CDK Tutorials

[Deploying with the AWS CDK](cdk.md)

: This tutorial walks you through creating a REST API with a DynamoDB data
  store that's deployed using the AWS CDK. It shows you how you can combine
  the APIs of Chalice with CDK construct APIs
