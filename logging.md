# Logging

- Multiple levels
- Dynamic control
- Tracebacks
- Higher-level combination with asserts

# Presenter notes

- Here's just a high-level view of some of the benefits of logging

--------------------------------------------------

# Logging levels

- Levels: exception, critical, warning, info...
- Temporarily cut down on debug noise
- Send levels to multiple locations

--------------------------------------------------

# Dynamic control

- Change log level dynamically
- Important with alternative distribution
    - Pyinstaller, py2exe

## Presenter notes

- Read log level from database/config file
- Dynamic control is big step over asserts
- Important b/c restarting interpreter could lose state/debug scenario

--------------------------------------------------

# Tracebacks

- Built-in with exception level
- Invaluable in error scenarios

--------------------------------------------------

# Logging + asserts

- Log assertions to different file/database
- Lots of data-mining capabilities

# Presenter notes

- Build a low-fi analytics system by logging to database, network file, dropbox
- Shell scripts to collect simple text files
- Track what features people use

--------------------------------------------------

# Logging + asserts

    !python
    def main():
        logging.basicConfig(level=logging.WARNING)
        log = logging.getLogger('example')
        try:
            throws()
            return 0
        except AssertionError:
            log.debug('Error: %s' % (err))
        except Exception as err:
            log.exception('Error from throws():')
            return 1

--------------------------------------------------

# Logging downsides

- Difficulty maintaining consistent levels
- Multiple loggers can be complicated
    - Logging cookbook
    - http://docs.python.org/2/howto/logging-cookbook.html

# Presenter notes

- Two CS problems, naming and caching
- Levels == naming
- Be careful/mindful logging could be your best defense against a production
  bug
