# Quickstart

In this tutorial, you'll use the `chalice` command line utility
to create and deploy a basic REST API.  This quickstart uses Python 3.10,
but AWS Chalice supports all versions of Python supported by AWS Lambda,
which includes Python 3.10 through Python 3.14.

To install Chalice, we'll first create and activate a virtual environment
in python3.10:

```console
$ python3 --version
Python 3.10.20
$ python3 -m venv .venv
$ . .venv/bin/activate
```

Next we'll install Chalice using `pip`:

```console
$ python3 -m pip install chalice
```

You can verify you have chalice installed by running:

```console
$ chalice --help
Usage: chalice [OPTIONS] COMMAND [ARGS]...
...
```


Credentials
-----------

Before you can deploy an application, be sure you have
credentials configured.  If you have previously configured your
machine to run boto3 (the AWS SDK for Python) or the AWS CLI then
you can skip this section.

If this is your first time configuring credentials for AWS you
can follow these steps to quickly get started:

```ini
$ mkdir ~/.aws
$ cat >> ~/.aws/config
[default]
aws_access_key_id=YOUR_ACCESS_KEY_HERE
aws_secret_access_key=YOUR_SECRET_ACCESS_KEY
region=YOUR_REGION (such as us-west-2, us-west-1, etc)
```

If you want more information on all the supported methods for
configuring credentials, see the
[boto3 docs](https://docs.aws.amazon.com/boto3/latest/guide/configuration.html).


Creating Your Project
---------------------

The next thing we'll do is use the `chalice` command to create a new
project:

```console
$ chalice new-project helloworld
```

This will create a `helloworld` directory.  Cd into this
directory.  You'll see several files have been created for you:

```console
$ cd helloworld
$ ls -la
drwxr-xr-x   .chalice
-rw-r--r--   app.py
-rw-r--r--   requirements.txt
```

You can ignore the `.chalice` directory for now, the two main files
we'll focus on is `app.py` and `requirements.txt`.

Let's take a look at the `app.py` file:

```python
from chalice import Chalice

app = Chalice(app_name='helloworld')


@app.route('/')
def index():
    return {'hello': 'world'}
```

The `new-project` command created a sample app that defines a
single view, `/`, that when called will return the JSON body
`{"hello": "world"}`.


Deploying
---------

Let's deploy this app.  Make sure you're in the `helloworld`
directory and run `chalice deploy`:

```console
$ chalice deploy
Creating deployment package.
Creating IAM role: helloworld-dev
Creating lambda function: helloworld-dev
Creating Rest API
Resources deployed:
  - Lambda ARN: arn:aws:lambda:us-west-2:123456789012:function:helloworld-dev
  - Rest API URL: https://abcd.execute-api.us-west-2.amazonaws.com/api/
```

You now have an API up and running using API Gateway and Lambda:

```console
$ curl https://abcd.execute-api.us-west-2.amazonaws.com/api/
{"hello": "world"}
```

Try making a change to the returned dictionary from the `index()`
function.  You can then redeploy your changes by running `chalice deploy`.

## Cleaning Up

If you're done experimenting with Chalice and you'd like to cleanup, you can
use the `chalice delete` command, and Chalice will delete all the resources
it created when running the `chalice deploy` command.

```
$ chalice delete
Deleting Rest API: abcd4kwyl4
Deleting function arn:aws:lambda:region:123456789012:function:helloworld-dev
Deleting IAM Role helloworld-dev
```

## Next Steps

At this point, there are several tutorials you can follow based on what
you're interested in:

- [Creating REST APIs](tutorials/basicrestapi.md) - Dive into more detail on
  how to create a REST API using Chalice. We'll explore URL parameters, error
  messages, content types, CORs, and more.
- [Event Sources](tutorials/events.md) - In this tutorial, we'll focus on
  difference event sources you can connect with a Lambda function other than a
  REST API with Amazon API Gateway.
- [Websockets](tutorials/wschat.md) - In this tutorial, we'll show you
  how to create a websocket API and create a sample chat application.

You can also jump into specific [topic guides](topics/index.md). These are
more detailed than the tutorials, and provide more reference style
documentation on specific features of Chalice.

And finally, you can look at the [API Reference](api.md) for detailed API
documentation for Chalice. This is useful if you know exactly what feature
you're using but need to lookup a specific parameter name or return value.
