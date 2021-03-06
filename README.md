# pine

A simple logging wrapper for Winston.


## Usage
```javascript
var pine = require('pine');

var log = pine();
log.info('Hello, world!');
log.error('This Department Has Worked %d Days Without Injury', 0);
```

```bash
[2014-05-22 21:00:39.704 UTC] - info: [26195:index.js] Hello, world!
[2014-05-22 21:00:39.705 UTC] - error: [26195:index.js] This Department Has Worked 0 Days Without Injury
```


### API
#### `pine([name] [,options])`
- `name` (optional, *String*) - If not provided, defaults to file path relative to parent package.
- `options` (optional, *Object*) - Same options as `pine.configure`. When provided will create logger with provided
settings, using configured global settings as defaults.

Invoke `pine` directly to get a logger instance. The API of the logger is determined by the configured levels, which defaults
to npm levels: silly, debug, verbose, info, warn, error. Additionally, there is a `log` method which accepts the desired
level as it's first argument. Each method also supports `util.format`-like string interpolation.

```javascript
var log = pine();
log.silly('Uptime: %d days', 10);
log.debug('Helpful information');
log.verbose('More information');
log.info('Did you know...');
log.warn('Well, actually...');
log.error('Iceberg!');
```


#### `pine.configure(options);`
- `options` (*Object*) - The default options which will be used for all loggers.

Set global logging settings, using built-in settings as defaults.

```javascript
pine.configure({

    // The root directory against which relative paths are calculated. Defaults to root of calling module.
    basedir: __dirname,

    // The winston levels to use. Defaults to `npm` levels.
    levels: undefined,

    // The colors to use. Defaults to `npm` colors.
    colors: undefined,

    // The transports to use, mapping the transport name to settings.
    transports: {
        console: {
            level: 'debug'
        }
    },

    // Transports to be used for logging exceptions. An object mapping the transport name to settings.
    exceptionHandlers: undefined
});
```


#### `pine.settings`
Read-only property of current global default settings.