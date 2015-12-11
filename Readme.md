# Overview
__mflow__ facilitates the handling of ZMQ data streams. It provides basic accounting and statistics on messages 
received/send as well as an easy way to handle new types of data streams.
 

# Usage

```python
stream = mflow.connect('tcp://sf-lc:9999')
message  = stream.receive()
stream.disconnect()
```