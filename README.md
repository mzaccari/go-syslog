go-syslog [![Build Status](https://travis-ci.org/mzaccari/go-syslog.svg?branch=master)](https://travis-ci.org/mzaccari/go-syslog) [![GoDoc](http://godoc.org/github.com/mzaccari/go-syslog?status.svg)](hhttps://godoc.org/gopkg.in/mzaccari/go-syslog.v2) [![GitHub release](https://img.shields.io/github/release/mzaccari/go-syslog.svg)](https://github.com/mzaccari/go-syslog/releases)
==============================

Syslog server library for go, build easy your custom syslog server over UDP, TCP or Unix sockets using RFC3164, RFC6587 or RFC5424

Installation
------------

The recommended way to install go-syslog

```
go get gopkg.in/mzaccari/go-syslog.v2
```

Examples
--------

How import the package

```go
import "gopkg.in/mzaccari/go-syslog.v2"
```

Example of a basic syslog [UDP server](example/basic_udp.go):

```go
channel := make(syslog.LogPartsChannel)
handler := syslog.NewChannelHandler(channel)

server := syslog.NewServer()
server.SetFormat(syslog.RFC5424)
server.SetHandler(handler)
server.ListenUDP("0.0.0.0:514")
server.Boot()

go func(channel syslog.LogPartsChannel) {
    for logParts := range channel {
        fmt.Println(logParts)
    }
}(channel)

server.Wait()
```

License
-------

MIT, see [LICENSE](LICENSE)
