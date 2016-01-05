# Overview
__mflow__ facilitates the handling of ZMQ data streams. It provides basic accounting and statistics on messages 
received/send as well as an easy way to handle different types of messages within a stream.
 

# Installation
The mflow package is available on [https://pypi.python.org](https://pypi.python.org/pypi/mflow) and can be installed via pip

```bash
pip install mflow
```

Right now mflow comes with following message type support:
* array-1.0
* bsr_m-1.0
* dheader-1.0 (Dectris Eiger)
* dimage-1.0 (Dectris Eiger)
* dseries_end-1.0 (Dectris Eiger)

# Usage

Connect/Create stream:

```python
stream = mflow.connect(address, conn_type="connect", mode=zmq.PULL, receive_timeout=None, queue_size=100)
```

Receive a message:

```python
message = stream.receive(self, handler=None)
```

The returned `message` object contains the current receiving  statistics in `message.statistics` and the actual 
message data in `message.data`.

If there should be no dynamic resolution of the message handler an explicit handler can be specified to handle the 
incoming message. 


Disconnecting stream:

```python
stream.disconnect()
```


Sending message (ensure that you specified the correct mode!):

```python
stream.send('message content', send_more=True)
```


Example:

```python
import mflow
stream = mflow.connect('tcp://sf-lc:9999')

# Receive "loop"
message  = stream.receive()
print(message.statistics.messages_received)

stream.disconnect()
```

## Advanced

Manually register more handlers that are not provided by this package (after creating the stream)

```python
stream.handlers['id'] = myhandler
```

# Development

Upload package to pypi.python.org

```bash
python setup.py sdist upload
```
