# Python logging — a basic implementation

---
## Introduction

Generating appropriate log is a primary necessity in a software application. The main benefits of a well configured log output in comparison of print statements are such as -

1. Provides diagnostic details like module name, line number, traceback, loglevel etc

2. Log stream can be directed to various output like file, central logging system, container log etc

3. Loglevel can be modified to control the log output, without modifying code & restarting application.

## Python Configuration

Below code create a basic logging configuration using python standard ‘Logging’ package.
```
import logging

loglevel = os.environ.get('loglevel','DEBUG').upper()
logging.basicConfig(filename='logfile.log',
format='%(asctime)s %(name)-8s %(levelname)-8s %(message)s',
datefmt='%m/%d/%Y %I:%M:%S %p',
level=loglevel)
```
Here we are setting some common options like log file name, attributes of log output, datetime format, loglevel. We are getting the loglevel from environment variable instead of providing fixed value.

Python logging package have following loglevel — `DEBUG, INFO, WARNING, ERROR, CRITICAL`, to be used accordingly. By setting the loglevel from environment variable, we can use the below workflow -

1. In a piece of code, we write a debug level log message to track an expected output
    ```
    logging.debug('Running for loop with {} value'.format(value))
    ```
2. In a exception case, we catch the exception and generate a ERROR level log
    ```
    logging.ERROR('Exception occurred, unable to process for {} value'.format(value))
    ```
3. Now, in development stage we would want to view both the logs. However in production, we will only be interested in the `ERROR` log. So, after deployment, we simply change the loglevel by running `export loglevel=ERROR` which will limit the log messages to `ERROR` type only. Again, if we want to debug the production application and want to view the `DEBUG` level as well, we can simple change the loglevel, without making any code or application state updates.

## References

1. [Python Logging documentation](https://docs.python.org/3/howto/logging.html)
2. [Loggy — python logging](https://www.loggly.com/ultimate-guide/python-logging-basics/)
