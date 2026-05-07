# AWS Chalice

<img src="img/chalice-logo.png" alt="AWS Chalice logo" style="display: block; width: 100%; max-width: 100%; margin: 0 0 1.5rem 0;">

<div class="grid cards" markdown>

-   **Python Serverless Microframework for AWS**

    Chalice lets you quickly create and deploy applications that use AWS Lambda, API Gateway, Amazon S3, Amazon SNS, Amazon SQS, and other AWS services.

    [Get started](quickstart.md) · [View API reference](api.md)

-   **Build serverless apps with plain Python**

    ```console
    $ chalice deploy
    ...
    https://endpoint/api
    ```

</div>

[![Package Version](https://img.shields.io/pypi/v/chalice.svg?style=flat)](https://pypi.python.org/pypi/chalice/)
[![Python Versions](https://img.shields.io/pypi/pyversions/chalice.svg?style=flat)](https://pypi.python.org/pypi/chalice/)
[![Documentation Status](https://readthedocs.org/projects/chalice/badge/?version=latest)](https://aws.github.io/chalice/?badge=latest)
[![License](https://img.shields.io/pypi/l/chalice.svg?style=flat)](https://github.com/aws/chalice/blob/master/LICENSE)

Chalice is a framework for writing serverless apps in Python. It allows you to quickly create and deploy applications that use AWS Lambda. It provides:

- A command line tool for creating, deploying, and managing your app.
- A decorator-based API for integrating with Amazon API Gateway, Amazon S3, Amazon SNS, Amazon SQS, and other AWS services.
- Automatic IAM policy generation.

## What can I build?

### REST APIs

```python
from chalice import Chalice

app = Chalice(app_name="helloworld")


@app.route("/")
def index():
    return {"hello": "world"}
```

### Scheduled tasks

```python
from chalice import Chalice, Rate

app = Chalice(app_name="helloworld")


@app.schedule(Rate(5, unit=Rate.MINUTES))
def periodic_task(event):
    return {"hello": "world"}
```

### S3 event handlers

```python
from chalice import Chalice

app = Chalice(app_name="helloworld")


@app.on_s3_event(bucket="mybucket")
def handler(event):
    print(f"Object uploaded for bucket: {event.bucket}, key: {event.key}")
```

### SQS queue consumers

```python
from chalice import Chalice

app = Chalice(app_name="helloworld")


@app.on_sqs_message(queue="my-queue-name")
def handler(event):
    for record in event:
        print(f"Message body: {record.body}")
```

And several other AWS resources. Once you've written your code, run `chalice deploy` and Chalice takes care of deploying your app.

```console
$ chalice deploy
...
https://endpoint/api

$ curl https://endpoint/api
{"hello": "world"}
```

Up and running in less than 30 seconds. Give this project a try and share your feedback with us on GitHub.

## Where should I go next?

<div class="grid cards" markdown>

-   **Quickstart**

    ---

    Create and deploy a basic REST API with the `chalice` command line utility.

    [Start the quickstart](quickstart.md)

-   **Tutorials**

    ---

    Step-by-step examples for REST APIs, WebSockets, events, custom domains, and CDK.

    [Browse tutorials](tutorials/index.md)

-   **Topics**

    ---

    Deep dives on routing, views, configuration, packaging, authorizers, events, testing, and more.

    [Explore topics](topics/index.md)

-   **API Reference**

    ---

    Reference documentation for the public classes and methods available in Chalice.

    [Read the API reference](api.md)

-   **Sample Apps**

    ---

    Full sample applications including a todo app and media query app.

    [View samples](samples/index.md)

-   **Changelog**

    ---

    See recent fixes, enhancements, and release notes.

    [Read the changelog](changelog.md)

</div>
