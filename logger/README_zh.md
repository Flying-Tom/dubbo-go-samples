# 日志使用

 该 samples 演示了如何使用 lumberjack 配置 dubbo-go logger

## 目录

* default:  默认打印到控制台
* level:    设置日志的隔离级别
* rolling:  输出到文件
* custom: 自定义 logger

### 默认配置

在配置文件中不添加 logger 配置日志将会打印到控制台, 也可在配置文件中配置日志, 可参照如下方式:

zap 日志格式和级别设置

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

### 设置隔离级别

```go
logger.SetLoggerLevel("warn")
```

### 输出到文件

在配置文件中的 logger 选项下添加 file 项

```yaml
  logger:
    file:
      name: logs.log
      max-size: 1
      max-age: 3
      max-backups: 5
      compress: false
```

### 自定义 logger

自定义 logger 需要实现 logger 包中的 logger 接口

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

然后调用 SetLogger 方法设置 logger

```go
logger.SetLogger(&customLogger{})
```
