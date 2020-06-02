---
layout: post
title:  "Handling Signals in Go"
date:   2020-06-02 22:15:16 +0100
categories: go
---
Being able to manage the signals in Go may improve the quality of programs by reducing unexpected behaviors. For example, when users hit ^C on the CLI app, the opened services such as HTTP server and database are not gracefully shutdown. This, in turn, leads to inaccurately handled server requests and memory leakage. The purpose of this article is to present a method that programmers can follow to manage signals.

Usually, communication between the application and kernel is done through system calls. However, Go employs channels that have different functions, one of which includes communicating signals to the application. Therefore, we will use channels to manage signals in Go. 

Everything we need is in the built-in signal package. First off, we must redirect the signals to us via channels:
```go
signalChannel := make(chan os.Signal, 1)
signal.Notify(signalChannel, os.Interrupt, syscall.SIGINT, syscall.SIGTERM)
```
The first line presented above creates a channel of os.Signal's. Next, by calling the function Notify from package signal we redirect the os.Interrupt, SIGINT and SIGTERM to our channel. In order for the application to listen to the signal, simply wait for the channel to receive one:
```go
sgn := <-signalChannel
log.Printf("Handling %s ...\n", sgn)
// Handle your service
```
The full example:
```go
package main

import (
    "log"
    "os"
    "os/signal"
    "syscall"
)

func main() {
    signalChannel := make(chan os.Signal, 1)
    signal.Notify(signalChannel, os.Interrupt, syscall.SIGINT, syscall.SIGTERM)
 
    sgn := <-signalChannel
    log.Printf("Handling %s ...\n", sgn)
    // Handle your service
}
```
Run the program and then hit CTRL+C to terminate it and see the result.

If for your reasoning you want to hand over again the handling to the system you can simply call the Stop function and pass the channel as an argument.
