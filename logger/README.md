# Log usage

The samples demonstrate how to configure dubbo-go logger using lumberjack

## Contents

* default: print to the console by default
* level:   set the isolation level of the log
* rolling: output to file
* custom: set custom logger

### print to the console by default

If you don't add a logger to the configuration file, the configuration log will be printed to the console. You can also configure the log in the configuration file. You can refer to the following method:

zap log format and level settings

```yaml
    logger:
      driver: zap
      level: info
      format: text
      appender: console
      file:
        name: logs.log
        max-size: 1
        max-age: 3
        max-backups: 5
        compress: false
```

### set isolation level

```go
logger.SetLoggerLevel("warn")
```

### output to file

Add the file item under the logger option in the configuration file

```yaml
  logger:
    file:
      name: logs.log
      max-size: 1
      max-age: 3
      max-backups: 5
      compress: false
```

### coustom logger

Custom logger needs to implement the logger interface in the logger package

```go
type Logger interface {
    Info(args ...interface{})
    Warn(args ...interface{})
    Error(args ...interface{})
    Debug(args ...interface{})
    Fatal(args ...interface{})

    Infof(fmt string, args ...interface{})
    Warnf(fmt string, args ...interface{})
    Errorf(fmt string, args ...interface{})
    Debugf(fmt string, args ...interface{})
    Fatalf(fmt string, args ...interface{})
}
```

Then call SetLogger method to set logger

```go
logger.SetLogger(&customLogger{})
```
