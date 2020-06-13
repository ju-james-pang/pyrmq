<!--suppress HtmlDeprecatedAttribute -->
<div align="center">
  <h1>PyRMQ</h1>
  <a href="https://mit-license.org" target="_blank"><img src="https://img.shields.io/badge/license-MIT-blue.svg?longCache=true&style=for-the-badge" alt="License"></a> 
  <a href="https://github.com/psf/black"><img alt="Code style: black" src="https://img.shields.io/badge/code%20style-black-000000.svg?longCache=true&style=for-the-badge"></a>
  <p>Python with RabbitMQ—simplified so you won't have to.</p>
</div>

## Development Status
**Note**: Currently under active development.

## Features
- Use out-of-the-box and thread-safe `Consumer` and `Publisher` classes created from `pika` for your projects and tests.
- Built-in retry-backoff logic for connecting, consuming, and publishing. 
- Works with Python 3.

## Getting Started
### Installation
PyRMQ is available at PyPi.
```shell script
pip install pyrmq
```
### Usage
#### Publishing
Just instantiate the feature you want with their respective settings.
PyRMQ already works out of the box with RabbitMQ's [default initialization settings](https://hub.docker.com/_/rabbitmq).
```python
from pyrmq import Publisher
publisher = Publisher(
    exchange_name="exchange_name",
    queue_name="queue_name",
    routing_key="routing_key",
)
publisher.publish({"pyrmq": "My first message"})
```
#### Consuming
Intantiating a `Consumer` automatically starts it in its own thread making it
non-blocking by default. When run after the code from before, you should be
able to receive the published data.
```python
from pyrmq import Consumer

def callback(data):
    print(f"Received {data}!")

Consumer(
    exchange_name="exchange_name",
    queue_name="queue_name",
    routing_key="routing_key",
    callback=callback
)
```

## Documentation
Complete document is found at https://pyrmq.readthedocs.io

 run build and generate coverage report.


## Testing
For development, just run:
```shell script
pytest
```
To test for all the supported Python versions:
```shell script
pip install tox
tox
```
To test for a specific Python version:
```shell script
tox -e py38
```

