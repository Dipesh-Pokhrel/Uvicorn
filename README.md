# Uvicorn


Uvicorn is an extremely fast ASGI server implementation that makes use of uvloop and HTTP tools. 
ASGI should contribute to the development of a Python web framework ecosystem that is highly competitive with Node and Go in terms of achieving high throughput in IO-bound contexts. It also supports HTTP/2 and WebSockets, which WSGI does not support.

**Documentation**: [https://www.uvicorn.org](https://uvicorn.org)

**Requirement**: Python 3.7+ (for python 3.6 support, install version 0.16.0.)

### Install using pip:
```shell
$ pip install uvicorn
```
**For Installing uvicorn with minimal (pure Python) dependencies:**
```shell
 $ pip install uvicorn[standard]
```
Installing uvicorn with ‘Cython-based’ dependencies (where possible) and “other optimal extras”

"Cython-based" in this context means that the event loop uvloop will be installed and used if possible.
* uvloop is a lightweight replacement for the built-in asyncio event loop. Cython is used to implement it. 
* Because it is pure Python, the built-in asyncio event loop serves as an easy-to-read reference implementation and is there for easy debugging.
* If possible, the http protocol will be handled by httptools.

Furthermore, "optional extras" means that, if possible, the WebSockets protocol will be handled by websockets (if you want to use wsproto, you'll need to install it manually).
* In development mode, the --reload flag will use watchgod.
* Colorama will be installed on Windows for the colored logs.
* If you use the -- env-file option, python-dotenv will be installed.
* PyYAML will be installed, allowing you to pass a.yaml file to --log-config if desired.

### Creating a Simple application Using Uvicorn:
```python
import uvicorn
async def app(scope, receive, send):
    assert scope['type'] == 'http'

    await send({
        'type': 'http.response.start',
        'status': 200,
        'headers': [
            [b'content-type', b'text/plain'],
        ],
    })
    await send({
        'type': 'http.response.body',
        'body': b'Hello, world!',
```
 #### Run the server
```shell
 $ uvicorn Uvicorn:app 
 ```
 
