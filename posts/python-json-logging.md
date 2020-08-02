# Python logging in JSON format
### Published at: 2/8/2020
---
Logging in python can be achieved using inbuilt `logging` module. However, analysing the text based logs like below, can become complicated for log aggregation tools like ELK, especially in a microservice architecture
```
2020-07-20 12:05:30,766 - __main__ - DEBUG - This is a debug message
``` 
Alternatively, if we manage to output logs as stream of json objects with pre-defined key-values, it becomes much easier to index & analyse in an organised manner. 

## Required package
One such python package, which enabled Json logging for python application is [https://github.com/thangbn/json-logging-python](https://github.com/thangbn/json-logging-python). Other similar solutions are also available.

## Install
- Using `pip`
```
pip install json-logging
```

## Example setup
- Create a genetic utility function to return a `logger` object

```
def get_logger():
    """
    Generic utility function to get logger object with fixed configurations
    :return:
    logger object
    """
    json_logging.ENABLE_JSON_LOGGING = True
    json_logging.init_non_web()
    logger = logging.getLogger(__name__)
    logging.basicConfig()
    json_logging.config_root_logger()
    logger.setLevel(logging.DEBUG)
    logging.addLevelName(logging.ERROR, 'error')
    logging.addLevelName(logging.WARNING, 'warning')
    logging.addLevelName(logging.INFO, 'info')
    logging.addLevelName(logging.DEBUG, 'debug')
    logger.addHandler(logging.NullHandler())
    return logger

```
- Create a `logger` object
```
logger = get_logger()
```
- Sample log generation code & output

```
logger.error(e)
```
```
{"written_at": "2020-08-01T19:39:45.359Z", "written_ts": 1596310785359963000, "msg": "Internal Server Error: /api/endpoint1/user_name", "type": "log", "logger": "django.request", "thread": "Thread-3", "level": "error", "module": "log", "line_no": 228, "exc_info": "Traceback (most recent call last):\n...", "filename": "log.py"}

```

## Ideas for advanced use
- In addition to general logs, we can also use log messages with custom key-values for specific insights about the application. For example, we can add some extra keys to keep track of inter-api response time & use it afterward to understand application performace.
```
logger.info("Fetched from apiA/search",
                       extra={'props':
                           {
                               'caller_api': 'apiA',
                               'receiver_api': 'apiB',
                               'receiver_endpoint': 'search',
                               'api_response_parsed_duration': 28
                           }
                       }
            )

```

## Conclusion
As json is one of the most flexible, portable & understandable data transfer format, it can provide immense benefit to use json logging for any application (including python).

